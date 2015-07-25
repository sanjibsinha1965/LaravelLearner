# A specimen of Registration Page #

{{ Form::open(array('url' => 'test/test')) }}
                {{ Form::label('username', 'User Name') }}
{{ Form::text('user') }}
{{ Form::label('secret', 'Super Secret') }}
{{ Form::password('secret') }}
{{ Form::submit('Send') }}
{{ Form::close() }}
