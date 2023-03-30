# cloudkey-certificate role for Ansible

A role to replace the snake-oil certificate on Unifi Cloudkey v2 with a regular certificate.

Compiled from the instructions found at [How to install a SSL Certificate on Unifi Cloud Key](https://community.ui.com/questions/How-to-install-a-SSL-Certificate-on-Unifi-Cloud-Key/944dbbd6-cbf6-4112-bff5-6b992fcbf2c4) on the Unifi community forums and [Adding a Commercial SSL Certificate to Cloud Key](https://www.reddit.com/r/Ubiquiti/comments/luxflo/adding_a_commercial_ssl_certificate_to_cloud_key/) on */r/Ubiquiti* for the "v2 firmware support".

SSH needs to be enabled from the cloudkey's top-level advanced settings. Deploying an SSH key for the root user is advised.

Intermediate certificates were loosely tested and should work if appended to the certificate file.

For administrators with a bit of experience in managing certificates, the process appears to be a lot less error-prone than the extremely detailed HOWTOs make it seem. It is, however, tragically ridiculous how the files in `/etc/ssl/private` have carefully crafted permissions and the "v2" files in `/data/unifi-core/config` then frivolously changed to `chmod 0644`. Welcome to the Unifi ecosystem.
