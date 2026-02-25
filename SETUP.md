# Astrav Consulting Website - Setup Instructions

## Contact Form Setup

The contact form is configured to send emails to: **info@astravconsulting.com**

### Option 1: Formspree (Recommended - Free & Easy)

1. Go to https://formspree.io/
2. Sign up for a free account
3. Create a new form
4. Set the email to: **info@astravconsulting.com**
5. Copy your form endpoint (looks like: `https://formspree.io/f/xyzabc123`)
6. In `contact.html`, replace `YOUR_FORM_ID` with your actual form ID:
   ```html
   <form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```

**That's it!** The form will now send emails to info@astravconsulting.com

### Option 2: Web3Forms (Alternative)

1. Go to https://web3forms.com/
2. Enter your email: **info@astravconsulting.com**
3. Get your access key
4. Update the form in `contact.html`:
   ```html
   <form action="https://api.web3forms.com/submit" method="POST">
     <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY">
     <!-- rest of form fields -->
   </form>
   ```

### Option 3: PHP Backend (If you have a server with PHP)

Create a file called `send-email.php`:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $firstName = htmlspecialchars($_POST['firstName']);
    $lastName = htmlspecialchars($_POST['lastName']);
    $email = htmlspecialchars($_POST['email']);
    $company = htmlspecialchars($_POST['company']);
    $phone = htmlspecialchars($_POST['phone']);
    $interest = htmlspecialchars($_POST['interest']);
    $message = htmlspecialchars($_POST['message']);
    
    $to = "info@astravconsulting.com";
    $subject = "New Contact Form Submission - Astrav Consulting";
    $body = "Name: $firstName $lastName\n";
    $body .= "Email: $email\n";
    $body .= "Company: $company\n";
    $body .= "Phone: $phone\n";
    $body .= "Interest: $interest\n\n";
    $body .= "Message:\n$message";
    
    $headers = "From: noreply@astravconsulting.com\r\n";
    $headers .= "Reply-To: $email\r\n";
    
    if (mail($to, $subject, $body, $headers)) {
        header("Location: contact.html?success=1");
    } else {
        header("Location: contact.html?error=1");
    }
}
?>
```

Then update the form action in `contact.html`:
```html
<form class="contact-form" action="send-email.php" method="POST">
```

## Files Included

- **index.html** - Homepage
- **services.html** - All services
- **managed-services.html** - 24×7 managed security
- **advisory.html** - Security assessments
- **about.html** - About/Why Astrav
- **contact.html** - Contact form
- **styles.css** - All styling

## Deployment

1. Upload all files to your web hosting
2. Make sure `styles.css` is in the same directory as the HTML files
3. Set up the contact form using one of the options above
4. Test the form to ensure emails arrive at info@astravconsulting.com

## Email Configuration

All email links throughout the site point to: **info@astravconsulting.com**

## Need Help?

If you need help setting up the form or have questions, the easiest option is **Formspree** - it takes 2 minutes and works immediately.
