<!DOCTYPE html>
<html>
<head>
<title>Laravel Sessions and Cookies</title>
<meta charset="utf-8">
</head>
<body>
<h2>Laravel Sessions and Cookies</h2>
<?= Form::open() ?>
<?= Form::label('email', 'Email address: ') ?>
<?= Form::text('email') ?>
<br>
<?= Form::label('name', 'Name: ') ?>
<?= Form::text('name') ?>
<br>
<?= Form::label('city', 'City: ') ?>
<?= Form::text('city') ?>
<br>
<?= Form::submit('Submit!') ?>
<?= Form::close() ?>
</body>
</html>
