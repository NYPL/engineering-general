# Sending Emails from an Application

Sometimes our applications need to send emails to the users. The emails could be a confirmation email after creating a new account, an account credential rescuing email, or a notification.

## SMTP Configurations

To keep our applications consistent, we SHOULD use our AWS SES service to manage the emails. The SMTP configurations SHOULD be,

Server Name: email-smtp.us-east-1.amazonaws.com
Port: 587
Use Transport Layer Security (TLS): Yes

And the authentication is the credentials created by SES Management Console. You can find them in our EC2 Parameter Store, under the name /production/ses/email-smtp.us-east-1.amazonaws.com/credentials. These credentials SHOULD be used for all the applications that send emails via the address email-smtp.us-east-1.amazonaws.com.

## Mail From Address

The sender MUST have the domain as _nypl.org_ with the name that indicates the application. For example, _repoapi@nypl.org_.
