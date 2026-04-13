FROM rockylinux/rockylinux:9-ubi-init AS htcondorce

# Enable HTCondor + HTCondor-CE repositories
RUN dnf -y install https://htcss-downloads.chtc.wisc.edu/repo/25.0/htcondor-release-current.el9.noarch.rpm

# Install HTCondor-CE
RUN dnf -y install htcondor-ce \
 && dnf clean all

# Create directories needed for K8s volumes
RUN mkdir -p /etc/condor/config.d \
             /var/log/condor \
             /var/lib/condor

# Expose CE ports
EXPOSE 9619 9618

# Entrypoint
CMD ["/usr/sbin/condor_master", "-f"]
