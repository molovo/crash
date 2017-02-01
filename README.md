# Crash

Proper error handling, exceptions and try/catch for ZSH

## Installation

### [zulu](https://github.com/zulu-zsh/zulu)

```sh
zulu install crash
```

### Manual

```sh
git clone https://github.com/molovo/crash crash
cp crash/crash /usr/local/share/zsh/site-functions # Or anywhere else in $fpath
```

## Usage

### Set up the global error handler

Crash comes with a global error handler, which prints a readable error and stack trace both for user-create exceptions and traditional shell exit codes.

```sh
autoload -Uz crash && crash register

throw TestException 'This is a test' # Will cause the error handler to be displayed
```

### Try/catch

Crash comes with the functions `try`, `catch` and `throw`, allowing you to handle exceptions much as you would in a 'proper' programming language.

```sh
autoload -Uz crash && crash register

# The function we're going to call
function do_something() {
  echo 'Start to do something...'
  throw RainbowException 'Unicorns!'
  echo 'This message will never be displayed'
}

# A function to handle any caught exceptions
function error_handler() {
  local exception="$1" message="${(@)@:2}"

  echo $exception # RainbowException
  echo $message   # Unicorns!
}

try do_something
catch RainbowException error_handler
```

## License

Copyright (c) 2016 James Dinsdale <hi@molovo.co> (molovo.co)

Crash is licensed under The MIT License (MIT)

## Team

* [James Dinsdale](http://molovo.co)
