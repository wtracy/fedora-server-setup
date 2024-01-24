# Fedora Server Setup

This is a collection of notes on setting up a Fedora-based server. They are intended for my personal use. If they're useful to someone else, cool.

## Firewall

```
sudo yum install firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld
sudo firewall-cmd --zone=public --permanent --add-service=ssh
sudo firewall-cmd --zone=public --permanent --add-service=http
sudo firewall-cmd --zone=public --permanent --add-service=httpd
sudo firewall-cmd --reload
```

## Encryption

I use Let's Encrypt and Certbot for my SSL certificates. Certbot has [excellent official instructions](https://certbot.eff.org/instructions?ws=apache&os=fedora).

## Backup

I use Restic to back up everything to Backblaze. Backblaze provides [instructions](https://www.backblaze.com/docs/cloud-storage-integrate-restic-with-backblaze-b2).

## Email

I currently use Postfix to forward email out through Sendgrid rather than trying to maintain my own outbound email server. Sendgrid has [instructions](https://docs.sendgrid.com/for-developers/sending-email/postfix).

Install the `mailx` package and use the `mail` command to test. (Though the default `sendmail` script seems to do the job?)

I'm potentially interested in switching to a more modern email daemon.

## Log monitoring

### Logwatch

You may need to [set up Cronie to run cronjobs](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/monitoring-and-automation/Automating_System_Tasks/) first.

```
sudo dnf install logwatch
```

Then update `/etc/logwatch/conf/logwatch.conf`. This file overrides defaults located in `/usr/share/logwatch/default.conf/logwatch.conf`. If nothing else, you will need to set up the To and From email addresses.

### Nagios

[Nagios](https://www.nagios.org).
