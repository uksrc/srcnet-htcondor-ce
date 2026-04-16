FROM rockylinux/rockylinux:9-minimal AS builder

# Enable HTCondor + HTCondor-CE repositories & install HTCondor-CE
RUN microdnf install -y dnf ; \
    microdnf -y install epel-release ; \
    /usr/bin/crb enable ; \
    dnf -y install https://htcss-downloads.chtc.wisc.edu/repo/25.0/htcondor-release-current.el9.noarch.rpm ; \
    dnf -y install htcondor-ce ; \
    dnf clean all ; \
    microdnf clean all ; \
    rm -rf /usr/share/doc/* /usr/share/man/* /var/cache/* /tmp/* || true

# Expose CE ports
EXPOSE 9619 9618

# Entrypoint
CMD ["/usr/sbin/condor_master", "-f"]
