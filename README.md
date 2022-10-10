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

## Interview questions

1. What’s the difference between the include() and require() functions?

_They both include a specific file but on require the process exits with a fatal error if the file can’t be included, while include statement may still pass and jump to the next step in the execution._

2. How can we get the IP address of the client?

```
$_SERVER["REMOTE_ADDR"];
```

3. What’s the difference between unset() and unlink()?

_unset() sets a variable to “undefined” while unlink() deletes a file we pass to it from the file system._

4. What are the main error types in PHP and how do they differ?

- Notices – Simple, non-critical errors that are occurred during the script execution. An example of a Notice would be accessing an undefined variable.
- Warnings – more important errors than Notices, however the scripts continue the execution. An example would be include() a file that does not exist.
- Fatal – this type of error causes a termination of the script execution when it occurs. An example of a Fatal error would be accessing a property of a non-existent object or require() a non-existent file.

5. What is the difference between GET and POST?

- GET displays the submitted data as part of the URL, during POST this information is not shown as it’s encoded in the request.
- GET can handle a maximum of 2048 characters, POST has no such restrictions.
- GET allows only ASCII data, POST has no restrictions, binary data are also allowed.
Normally GET is used to retrieve data while POST to insert and update.

6. How can you enable error reporting in PHP?

_Check if “display_errors” is equal “on” in the php.ini or declare “ini_set('display_errors', 1)” in your script.
Then, include “error_reporting(E_ALL)” in your code to display all types of error messages during the script execution._

7. What are Traits?

_Traits are a mechanism that allows you to create reusable code in languages like PHP where multiple inheritance is not supported. A Trait cannot be instantiated on its own._

8. Can the value of a constant change during the script’s execution?

_No, the value of a constant cannot be changed once it’s declared during the PHP execution._

9. Can you extend a Final defined class?

_No, you cannot extend a Final defined class. A Final class or method declaration prevents child class or method overriding._

10. What are the __construct() and __destruct() methods in a PHP class?

_All objects in PHP have Constructor and Destructor methods built-in. The Constructor method is called immediately after a new instance of the class is being created, and it’s used to initialize class properties. The Destructor method takes no parameters. Understanding these two in PHP means that the candidate knows the very basics of OOP in PHP._

11. How we can get the number of elements in an array?

_The count() function is used to return the number of elements in an array._

12. How would you declare a function that receives one parameter name hello?

```
<?php
function showMessage($hello=false){
  echo ($hello)?'hello':'bye';
}
?>
```

13. The value of the variable input is a string 1,2,3,4,5,6,7. How would you get the sum of the integers contained inside input?

```
<?php
echo array_sum(explode(',',$input));
?>
```

14. Suppose you receive a form submitted by a post to subscribe to a newsletter. This form has only one field, an input text field named email. How would you validate whether the field is empty? Print a message "The email cannot be empty" in this case.

```
<?php
if(empty($_POST['email'])){
  echo "The email cannot be empty";
}
?>
```

15. What does MVC stand for and what does each component do?

_MVC stands for Model View Controller. The controller handles data passed to it by the view and also passes data to the view. It’s responsible for the interpretation of the data sent by the view and dispersing that data to the appropriate models awaiting results to pass back to the view. Very little, if any business logic should be occurring in the controller.

The model’s job is to handle specific tasks related to a specific area of the application or functionality. Models will communicate directly with your database or other storage system and will handle business logic related to the results.

The view is passed data by the controller and is displayed to the user.

Overall, this question is worth knowing as the MVC design pattern has been used a lot in the last few years and is a very good design pattern to know. Even with more advanced flows that go down to repositories and entities, they still are following the same basic idea for the Controller and View.

The Model is typically just split out into multiple components to handle specific tasks related to database data, business logic etc. The MVC design pattern helps draw a better understanding of what is being used, as a whole, in the industry._

16. How does one prevent the following Warning ‘Warning: Cannot modify header information – headers already sent’ and why does it occur in the first place?

_The candidate should not output anything to the browser before using code that modifies the HTTP headers. Once the developer calls echo or any other code that clears the buffer, the developer can no longer set cookies or headers._

17. What are SQL Injections, how do you prevent them and what are the best practices?

_SQL injections are a method to alter a query in a SQL statement send to the database server. That modified query then might leak information like username/password combinations and can help the intruder to further compromise the server.

To prevent SQL injections, one should always check & escape all user input. In PHP, this is easily forgotten due to the easy access to $_GET & $_POST, and is often forgotten by inexperienced developers. But there are also many other ways that users can manipulate variables used in a SQL query through cookies or even uploaded files (filenames). The only real protection is to use prepared statements everywhere consistently.

Do not use any of the mysql_* functions which have been deprecated since PHP 5.5 ,but rather use PDO, as it allows you to use other servers than MySQL out of the box. mysqli_* are still an option, but there is no real reason nowadays not to use PDO, ODBC or DBA to get real abstraction. Ideally you want to use Doctrine or Propel to get rid of writing SQL queries all together and use object-relational mapping which binds rows from the database to objects in the application._

18. Why would you use === instead of ==?

_If you would want to check for a certain type, like an integer or boolean, the === will do that exactly like one would expect from a strongly typed language, while == would convert the data temporarily and try to match both operand’s types.

The identity operator (===) also performs better as a result of not having to deal with type conversion. Especially when checking variables for true/false, one should avoid using == as this would also take into account 0/1 or other similar representation._

19. What are PSRs? Choose 1 and briefly describe it.

_PSRs are PHP Standards Recommendations that aim at standardizing common aspects of PHP Development._

20. What PSR Standards do you follow? Why would you follow a PSR standard?

_One should follow a PSR because coding standards often vary between developers and companies. This can cause issues when reviewing or fixing another developer’s code and finding a code structure that is different from yours. A PSR standard can help streamline the expectations of how the code should look, thus cutting down confusion and in some cases, syntax errors._

21. Do you use Composer? If yes, what benefits have you found in it?
22. What’s the difference between using mysql_ functions and PDO?
23. Describe how inheritance works with PHP.
24. Do you know what the PHP-FIG is? Describe it, describe the PSRs you know.
25. What classes would you create to build a basic Twitter-style status system with OOP?
26. What frameworks are you experienced in?
27. What frameworks do you prefer? Why?
28. Thoughts/experience with unit testing?

## References

- https://www.php.net/manual/en/
- https://phpbestpractices.org/
- https://arc.dev/developer-blog/php-interview-questions/
