---
title: 'Sending Email'
intro: Be sure to configure your email settings if you want to invite new users, send password resets, and receive form submission notifications. There's even an adorable little test utility in the control panel to help you with a double-check.
template: page
id: bd1261de-7c4c-4c22-baf5-8a52cdd10c74
blueprint: page
stage: 4
---
## Overview

Statamic taps into Laravel's clean, simple API over the popular [SwiftMailer][swiftmailer] library (don't worry, the library is better than the neglected webpage) with drivers for SMTP, Mailgun, Postmark, Amazon SES, and `sendmail`, allowing you to quickly get started sending mail through a local or cloud based service of your choice.

## Configuring

Your mail settings are located in `config/mail.php` and pre-wired to use [environment variables](/configuration#environment-variables) so you can easily swap out providers and keep credentials safe and out of your project files.


## Drivers

The API based drivers like Mailgun and Postmark are often simpler and faster than SMTP servers. If possible, you should use one of these drivers. All of the API drivers require the Guzzle HTTP library, which may be installed via the Composer package manager:

``` bash
composer require guzzlehttp/guzzle
```

For specific driver configuration details, reference the [Laravel Mail Driver documentation](https://laravel.com/docs/mail#driver-prerequisites).

## Testing

There's an email utility in the control panel to help you easily test your email settings. Enter an email address (preferably your own) and click **Send Test Email** and wait. If you don't get anything before your birthday you know your settings need tweaking.

<figure>
    <img src="/img/email-utility.png" alt="Email Utility" width="480">
    <figcaption>Is email working? Click to find out!</figcaption>
</figure>


[swiftmailer]: https://swiftmailer.symfony.com
