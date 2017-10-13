# The purpose of this Docker image

I created this image because the [official PHP repository](https://hub.docker.com/_/php/) on Docker Hub doesn't have any MTA (Mail Transfer Agent) installed, meaning that the `mail()` PHP function won't work and cause this peculiar error:

```bash
WARNING: [pool www] child 6 said into stderr: "sh: 1: -t: not found"
```

This repository adds a simple SMTP client, *msmtp*, so that you can transmit mail to an SMTP server (for example at a free mail provider, like Gmail) which takes care of further delivery.

Read more about *msmtp* here: [http://msmtp.sourceforge.net/](http://msmtp.sourceforge.net/).

## Working example

This example is similar to how you'd run it in a production setting, except that for testing purposes we call the `send.php` file directly via `docker exec` and not through a webserver like nginx. It uses Docker *swarm mode* (17.06+), so make sure you run `docker swarm init` before you begin.

1. Clone the GitHub repo: `git clone https://github.com/ilyasotkov/docker-php-msmtp.git`, then `cd docker-php-msmtp/example`.
2. Open the `msmtprc` file and replace `example@gmail.com` with an address of your Gmail account. Testing mail will be sent from this address.
3. Add the Gmail account's password to `gmail_password` file. A *Docker secret* will be created from that file.
4. Modify `send.php` and replace `your-mailbox@example.com` with an email address that you indend receiving email to.
5. Run `docker stack deploy -c docker-stack.yaml mailer`. You PHP service is now running. Run `docker ps` to check the container is up and grab its ID for the next step.
6. You can now test sending email by running `docker exec <container id> php /send.php`. Check your mailbox now!
