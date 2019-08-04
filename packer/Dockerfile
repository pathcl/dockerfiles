# Choose packer 1.3.3 as the version
ARG         packer_version=1.3.3@sha256:e65fb210abc027b7d66187d34eb095fffa2fd8401e7032196f760d7866c6484c
FROM	    hashicorp/packer:${packer_version} AS packer
FROM	    alpine:3.9

# Add utilities used inside later Packer builds. Proxy settings
RUN         apk add --update bash jq wget curl
COPY 	    --from=packer /bin/packer /bin/packer

# Download the Packer vSphere builders from the JetBrains infra repo
ARG         vsphere_packer_builders_version=v2.3
ADD         https://github.com/jetbrains-infra/packer-builder-vsphere/releases/download/${vsphere_packer_builders_version}/packer-builder-vsphere-clone.linux /bin/packer-builder-vsphere-clone.linux
ADD         https://github.com/jetbrains-infra/packer-builder-vsphere/releases/download/${vsphere_packer_builders_version}/packer-builder-vsphere-iso.linux /bin/packer-builder-vsphere-iso.linux

# Exec permissions
RUN         chmod +x /bin/packer-builder-vsphere-iso.linux /bin/packer-builder-vsphere-clone.linux

# Set the entrypoint to run Packer by default
ENTRYPOINT  [ "/bin/packer" ]
