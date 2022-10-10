# PHP

PHP (recursive acronym for PHP: Hypertext Preprocessor) is a widely-used open source general-purpose scripting language that is especially suited for web development and can be embedded into HTML.

***I've been using PHP since 2002 to build web projects***

## Best Practices

### Coding

1. Use <?php ?>
2. Use spl_autoload_register() to register your auto-load function.
3. Single vs. double quotes from a performance perspective. It doesn’t really matter.
4. define() vs. const Use define() unless readability, class constants, or micro-optimization are concerns.
5. Caching PHP opcode. Lucky you: PHP has a built-in opcode cache!
6. PHP and Memcached. If you need a distributed cache, use the Memcached client library. Otherwise, use APCu.
7. PHP and regex Use the PCRE (preg_*) family of functions.
8. Sending email Use PHPMailer. PHPMailer is a popular and well-aged open-source library that provides an easy interface for sending mail securely. It takes care of the gotchas for you so you can concentrate on more important things.

```
<?php
// Include the PHPMailer library
require_once('phpmailer-5.2.7/PHPMailerAutoload.php');
 
// Passing 'true' enables exceptions.  This is optional and defaults to false.
$mailer = new PHPMailer(true);
 
// Send a mail from Bilbo Baggins to Gandalf the Grey
 
// Set up to, from, and the message body.  The body doesn't have to be HTML; check the PHPMailer documentation for details.
$mailer->Sender = 'bbaggins@example.com';
$mailer->AddReplyTo('bbaggins@example.com', 'Bilbo Baggins');
$mailer->SetFrom('bbaggins@example.com', 'Bilbo Baggins');
$mailer->AddAddress('gandalf@example.com');
$mailer->Subject = 'The finest weed in the South Farthing';
$mailer->MsgHTML('<p>You really must try it, Gandalf!</p><p>-Bilbo</p>');
 
// Set up our connection information.
$mailer->IsSMTP();
$mailer->SMTPAuth = true;
$mailer->SMTPSecure = 'ssl';
$mailer->Port = 465;
$mailer->Host = 'my smtp host';
$mailer->Username = 'my smtp username';
$mailer->Password = 'my smtp password';
 
// All done!
$mailer->Send();
?>
```

9. Validating email addresses Use the filter_var() function.
10. Sanitizing HTML input and output Use the htmlentities() function for simple sanitization and the HTML Purifier library for complex sanitization.
11. PHP and UTF-8 There’s no one-liner. Be careful, detailed, and consistent.
12. Working with dates and times Use the DateTime class.
13. Checking if a value is null or false Use the === operator to check for null and boolean false values.
14. Connecting to and querying a MySQL database, use PDO and its prepared statement functionality.

### Passwords

Hashing is the standard way of protecting a user’s password before it’s stored in a database. Many common hashing algorithms like md5 and even sha1 are unsafe for storing passwords, because hackers can easily crack passwords hashed using those algorithms.

PHP provides a built-in password hashing library that uses the bcrypt algorithm, currently considered the best algorithm for password hashing.

```
<?php
// Hash the password.  $hashedPassword will be a 60-character string.
$hashedPassword = password_hash('my super cool password', PASSWORD_DEFAULT);
 
// You can now safely store the contents of $hashedPassword in your database!
 
// Check if a user has provided the correct password by comparing what they typed with our hash
password_verify('the wrong password', $hashedPassword); // false
 
password_verify('my super cool password', $hashedPassword); // true
?>
```

Many sources will recommend that you also “salt” your password before hashing it. That’s a great idea, and password_hash() already salts your password for you. That means that you don’t have to salt it yourself.

## References

- https://www.php.net/manual/en/
- https://phpbestpractices.org/
