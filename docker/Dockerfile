FROM rockylinux/rockylinux:9-minimal AS builder

# Enable HTCondor + HTCondor-CE repositories & install HTCondor-CE
RUN microdnf -y install https://htcss-downloads.chtc.wisc.edu/repo/25.0/htcondor-release-current.el9.noarch.rpm ; \
    microdnf -y install htcondor-ce ; \
    microdnf clean all ; \
    rm -rf /usr/share/doc/* /usr/share/man/* /var/cache/* /tmp/* || true

FROM rockylinux/rockylinux:9-minimal

# Copy installed HTCondor-CE files from builder stage
COPY --from=builder /usr /usr
COPY --from=builder /etc/condor /etc/condor
COPY --from=builder /var/lib/condor /var/lib/condor
COPY --from=builder /lib64 /lib64

# Expose CE ports
EXPOSE 9619 9618

# Entrypoint
CMD ["/usr/sbin/condor_master", "-f"]
