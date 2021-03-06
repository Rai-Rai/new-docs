# Leaf Forms

Since v1.5.0 Leaf Form has totally replaced Simple Validation from v1.2.0 which was discontinued in v1.3.0. Leaf Form contains methods to simply and quickly handle input from the user.

To use Leaf Form, you simply have to import it:

```js
$form = new Leaf\Form;
```

## Leaf Form Methods

### sanitizeInput

sanitizeInput offers basic security for input data, i.e. sanitizing input against SQL injection.

```js
$username = $form->sanitizeInput($username);
```

### isEmpty

isEmpty checks a field to see if it's empty. If it's empty, it throws an error (the error message passed). It takes in 2 parameters: the data to test and the error message if it's empty(optional).

```js
$form->isEmpty($username); // error will be: This field is required
$form->isEmpty($username, "Username is required");
```

### isNull

isNull checks a field to see if it's null. If it's null, it throws an error (the error message passed). It takes in 2 parameters: the data to test and the error message if it's null(optional).

```js
$form->isNull($username); // error will be: This field cannot be null
$form->isNull($username, "Username can't be null");
```

### <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span> Form Submit

This creates a form and submits it. You can call it a virtual form.  It takes in 3 parameters, the request type, the form action and the form data. Currently, it only supports GET and POST requests.

```js
$form->submit("POST", "/book/create", [
	"title" => "Book One",
	"author" => "Mychi"
]);
```

### Validate

Leaf now provides a much simpler way to validate a parameter using Leaf Forms. In one line, you can create a bunch of rules to validate a parameter with. Validate simply makes sure that the passed selected parameters pass these validation tests. It's never been simpler😎

Parameters which fail the form validation are saved in the form's errors which can be accessed with errors(). So In case the validation fails, `validate` returns false, else true.

```js
$form->validate([
	"username" => "validUsername",
	"email" => "email",
	"password" => "required"
]);
```

##### <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span> Multiple Rule Validation

You can now pass an array as the rule parameter. If there's more than one, rule, both of them will apply. Also, pls make sure not to use contradictory rules like `number` and `textOnly` or `validUsername` and `email`.

```js
$form->validate([
	"username" => "validUsername",
	"email" => "email",
	"password" => ["required", "noSpaces"]
]);
```

This is a list of all supported validate rules

- required: field is required
- number: must only contain numbers
- textOnly: should be text **only**, no spaces allowed
- validUsername: must only contain characters 0-9, A-Z and _
- email: must be a valid email
- NoSpaces: can't contain any spaces
- <span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 10px;">New in v2</span> text : must only contain text and spaces

**Note that these rules aren't case-sensitive, so you can write them however you want, as long as the spelling is the same.**

### errors

Remember we talked about Leaf Form errors? Leaf Form holds errors for all failed tests, you get all these errors back with returnErrors

```js
$form->isNull($username, "username", "Username can't be null");

$errors = $form->errors();

return $errors;
```

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>