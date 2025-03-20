# cloudkey-certificate role for Ansible

A role to replace the snake-oil certificate on Unifi Cloudkey v2 with a regular certificate.

Compiled from the instructions found at [How to install a SSL Certificate on Unifi Cloud Key](https://community.ui.com/questions/How-to-install-a-SSL-Certificate-on-Unifi-Cloud-Key/944dbbd6-cbf6-4112-bff5-6b992fcbf2c4) on the Unifi community forums and [Adding a Commercial SSL Certificate to Cloud Key](https://www.reddit.com/r/Ubiquiti/comments/luxflo/adding_a_commercial_ssl_certificate_to_cloud_key/) on */r/Ubiquiti* for the "v2 firmware support".

For administrators with a bit of experience in managing certificates, the process appears to be a lot less error-prone than the extremely detailed HOWTOs make it seem. 

SSH needs to be enabled from the cloudkey's top-level advanced settings. Deploying an SSH key for the root user is advised.

Intermediate certificates were loosely tested and should work if appended to the certificate file.

## Lifecycle

* My certificate disappeared without a trace during a reboot one week before(!) its expiration and was replaced with a newly created self-signed snake-oil cert. 
  * After the not-yet expired certificate was re-deployed using this playbook, it disappeared after another reboot, replaced with yet another newly generated snake-oil cert.
  * No further automatic replacement occurred after deploying a new certificate.
  * This replacement is initiated from within the core node app */usr/share/unifi-core/app/service.js*. A permanent workaround should probably move towards dedicated certificate names and override things in or around nginx's */data/unifi-core/config/http/local-certs.conf*.

## Troubleshooting notes

I believe the keystore in */etc/ssl/private* is not used anymore. However:

```
openssl pkcs12 -in /etc/ssl/private/unifi.keystore.jks -passin pass:aircontrolenterprise -nokeys
openssl x509 -in /data/unifi-core/config/unifi-core.crt -noout -subject -issuer
```

## Status

* Confirmed still working on 2025-03-20
