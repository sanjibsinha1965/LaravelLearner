# A specimen of Form BUilder #
{{ Form::open(array('url' => 'home/regis')) }}

{{-- Username field. ------------------------}}
{{ Form::label('username', 'Username') }}
{{ Form::text('username') }}

{{-- Email address field. -------------------}}
{{ Form::label('email', 'Email address') }}
{{ Form::email('email') }}

{{-- Password field. ------------------------}}
{{ Form::label('password', 'Password') }}
{{ Form::password('password') }}

{{-- Password confirmation field. -----------}}
{{ Form::label('password_confirmation', 'Password confirmation') }}
{{ Form::password('password_confirmation') }}

{{-- Form submit button. --------------------}}
{{ Form::submit('Register') }}


{{ Form::close() }}
