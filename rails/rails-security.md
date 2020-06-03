# Rails Security

[http://guides.rubyonrails.org/security.html](http://guides.rubyonrails.org/security.html)

## Example Security Problems:

## XSS

Cross Site Scripting Someone enters this into an unprotected webform for a blog comment:

```text
<script>
window.location = "https://myunsecuresite.com";
</script>
```

Whoever loads this page's blog will also load this person's comment.

Their window location will be changed.

## CSRF

Example exploit: Your torrent app is running on local host. It has a GUI that accepts requests to it for setting various things, like the admin password.

Someone posts this image in a forum:

```text
<img src="http://localhost:8080/gui/?action=setsetting&s=webui.password&v=eviladmin
" />
```

Makes a GET request to: [http://localhost:8080/gui/](http://localhost:8080/gui/) With the parameters:

* action=setsettings
* s=webui.password
* v=eviladmin

## SQL Injection

#### Where 1 = 1

In sql, 1=1 returns true for that table and returns everything in that table.

```text
name = request.body['user_id'];

query = "SELECT * FROM Users WHERE name = '" + name + "'";

//name ==> ' OR 1=1 --'
```

[https://github.com/wdi-sg/express-reference/blob/security/index.js\#L124](https://github.com/wdi-sg/express-reference/blob/security/index.js#L124)

#### Batched SQL Queries

If the database accepts queries that are grouped together:

```text
user_id = request.body['user_id'];

query = "SELECT * FROM Users WHERE UserId = " + user_id;

//user_id ==> 105; DROP TABLE Users
```

## Security Solutions

### CSRF Tokens

[http://guides.rubyonrails.org/security.html\#csrf-countermeasures](http://guides.rubyonrails.org/security.html#csrf-countermeasures)

\[[https://www.owasp.org/index.php/Cross-Site\_Request\_Forgery\_\(CSRF\)\]\(https://www.owasp.org/index.php/Cross-Site\_Request\_Forgery\_\(CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF%29]%28https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF)\)\)

## String Sanitization

What happens when you put HTML in a form?

What does the saved thing look like when you look at it in the show route?

Rails uses "html escaping" to clean up the stuff you finally see on the screen.

String sanitization in javascript is hard: [https://hackerfall.com/story/you-can-do-anything-in-javascript-with-only-an](https://hackerfall.com/story/you-can-do-anything-in-javascript-with-only-an)

### Don't use string interpolation with where

[http://guides.rubyonrails.org/security.html\#sql-injection](http://guides.rubyonrails.org/security.html#sql-injection)

### Don't Trust User Input

