# Sending emails through Gmail in Laravel


Sending emails through Gmail in Laravel is straightforward and requires a few setup steps to integrate Gmail's SMTP server with your Laravel application.

<!--more-->

## Step 1: Create app password for Gmail:
- Logging into your Google account.
- Navigate to **Security** settings, then select **2-Step Verification**.
- At the bottom of page, choose **App passwords**.
- Generate a new **app password**. This password will be used in your Laravel application's configuration.
- **Notice information** from Google: App passwords help you sign into your Google Account on older apps and services that don’t support modern security standards. App passwords are less secure than using up-to-date apps and services that use modern security standards. Before you create an app password, you should check to see if your app needs this in order to sign in.

## Step 2: Edit your `.env` file:
```dotenv
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD="YOUR-APP-PASSWORD"
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=your-email@gmail.com
MAIL_FROM_NAME="${APP_NAME}"
```
Replace `your-email@gmail.com` with your Gmail address and `YOUR-APP-PASSWORD` with the app password you generated.

## Step 3: Send a test email from Tinker:
- Open your terminal and run `php artisan tinker`.
- Use the following code to send a test email:
```php
use Illuminate\Support\Facades\Mail;

Mail::raw('Test email message from Laravel.', function ($message) {
    $message->to('recipient@gmail.com')->subject('Test email message from Laravel');
});
```
Replace `'recipient@gmail.com'` with the recipient's email address. This code sends a simple email message using Laravel's Mail facade.

**Conclusion:**
By following these steps, you've successfully configured Laravel to send emails via Gmail. This setup ensures reliable email delivery from your Laravel application using Gmail's SMTP server.
