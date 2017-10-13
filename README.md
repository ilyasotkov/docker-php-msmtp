# About this Repo

The [official PHP repository](https://hub.docker.com/_/php/) on Docker Hub doesn't have any MTA (Mail Transfer Agent) installed, meaning that the `mail()` PHP function won't work and cause this peculiar error:

```bash
`WARNING: [pool www] child 6 said into stderr: "sh: 1: -t: not found"`
```

This repository adds a simple SMTP client, *msmtp*, so that you can transmit mail to an SMTP server (for example at a free mail provider, like Gmail) which takes care of further delivery.

Read more about *msmtp* here: [http://msmtp.sourceforge.net/](http://msmtp.sourceforge.net/).

## Working example

1. Clone this repository and `cd ./example`.
2. Open the `msmtprc` file and replace `example@gmail.com` with an address of a Gmail account. Email will be sent from this address.
3. Add the Gmail account's password to `gmail_password` file.
4. Modify `send.php` and replace `your-mailbox@example.com` with an email address that you indend receiving email to.
5. Run `docker stack deploy -c docker-stack.yaml mailer`. You PHP service is now running. Run `docker ps` to check the container is up and grab its *ID* for the next step.
6. You can now test sending email by running `docker exec <container id> php /send.php`. Check your mailbox!
