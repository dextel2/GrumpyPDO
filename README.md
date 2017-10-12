# GrumpyPDO
A simple PHP class wrapper for PDO.

## Background

One of my biggest projects used to use a PHP database interface called SQLite, which has a function called [querysingle](http://php.net/manual/en/sqlite3.querysingle.php).
Well, for this project I decided that I wanted to switch to using MySQL, which obviously does not support the SQLite interface, and I needed to choose between `mysqli_*` and PDO.
I started with `mysqli_*` as I had already used it before, but I had zero experience with Prepared Statements, and I wanted my application to have good security, so I tried my hand at prepared statements with `mysqli_*` which worked but I didn't like the syntax, I didn't like the way the interface worked. So I tried PDO, which to me was much easier than `mysqli_*` prepared statements, and the syntax was a bit better.

After refactoring so many SQLite statements to PDO, I realized there wasn't really an alternative to SQLite's querysingle function. I also realized that my code was a bit longer than it used to be, because every statement needed parameters to be binded seperately from the query itself. This is when I wrote a simple function that I believe made my syntax **easier to read**, **easier to use**, and most importantly **more secure** as I'm effectively able to use prepared statements in a way that is more comfortable, thus making me more likely to use them more often and whenever necessary.

This function has helped me out tremendously, but I have since converted it into an actual class, which is what this project is.

## Installation Instructions

This project is simply 1 file, `grumpypdo.php`.

All you need to do is download the file (or copy it's contents and put them in your own file), include the file on the page, and then initialize a variable while calling the class.

```
include "grumpypdo.php";
$db = new GrumpyPDO("localhost", "username", "password", "database");
```

## Simple Usage Instructions

I wrote this class going for simplicity. As such, it is very easy to use. This is some basic ways that you can use this class, but some more complicated things may be documented in the wiki.

### Select & Loop

When I was researching PDO and mysqli_*, I had a hard time figuring out how to do simple things like looping through results from a query (Using prepared statements). There were few straightforward answers for this, so I'm going to try to explain it the best I can.

Now I remember when I first used mysqli_* you would use a while statement, and it's pretty easy to do, but not as easy with prepared statements. Here is how you do it with my function. Let's say we have these headers:

Table Name: **users**

| uid | fname | lname |
| --- | --- | --- |
| 1 | John | Doe |
| 2 | Jane | Doe |
| 3 | Oswald | Trackt |
| 4 | John | Baldwin |

Let's start with selecting all columns.

```
$db->query("SELECT * FROM users")->fetchAll();
```

Notice I used `fetchAll()` after the query, this is a "PDOStatement". Because the class returns the query as an object, you can use native PDO statement types, making this solution very powerful.
[Here is some more PDOStatements that can be used with this class](http://php.net/manual/en/class.pdostatement.php)

Moving on, the above query will return an array of values. This array will look like this:

```
Array
(
    [0] => Array
        (
            [uid] => 1
            [fname] => John
            [lname] => Doe
        )

    [1] => Array
        (
            [uid] => 2
            [fname] => Jane
            [lname] => Doe
        )

    [2] => Array
        (
            [uid] => 3
            [fname] => Oswald
            [lname] => Trackt
        )

    [3] => Array
        (
            [uid] => 4
            [fname] => John
            [lname] => Baldwin
        )

)
```

And from there, all you really need to do is loop through the array like any other PHP array. In other interfaces I have mostly seen people use while loops to get through their data, but for this data you can use a for loop or a foreach loop, which I find easier and cleaner.


# Contributors
Project Founder - [GrumpyCrouton](https://stackoverflow.com/users/5827005/grumpycrouton)

If you would like to help contribute to this project, please let me know.
