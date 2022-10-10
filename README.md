# PHP

PHP (recursive acronym for PHP: Hypertext Preprocessor) is a widely-used open source general-purpose scripting language that is especially suited for web development and can be embedded into HTML.

***I've been using PHP since 2002 to build web projects***

## Best Practices

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
