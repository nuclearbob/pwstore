# pw.py
A cli password manager in python. Inspired by password-store[[1]] by Jason A.
Donenfeld.

## Usage
```
$ ./pw.py -?
Usage: pw.py [OPTIONS] RECORD COMMAND [ARGS]...

Options:
  -?, -h, --help  Show this message and exit.

Commands:
  add     Create a new record
  alias   Create a symlink named ALIAS
  delete  Delete KEY from a record
  drop    Delete an entire record from the disk
  get     Retrieve a KEY value from a record
  list    List the keys in a record
  qrcode  Display a KEY value as a qrcode
  select  Decrypt a record and print it raw
  update  Update a record's KEY with VALUE
```

### Dependencies
The following non-standard dependencies are required:
```
pip install python-gnupg dulwich
```

There is an optional dependency to display passwords as QRcodes:
```
pip install pyqrcode
```
### GPG
Like password-store, pw.py uses GPG encryption to store data securely.  For
now, you must set your recipient key in the environment:

```
export PWSTORE_KEY='0xA96895ACB7F4970C'
```

### Examples
#### Create a new record
```
pw github.com add
```

#### Create an alias
```
pw github.com alias github
```

#### Add a password
```
pw github update password "$(apg -n1)"
```

#### Add some metadata
```
pw github update login_url "http://github.com"
pw github update username rpdelaney
```

## Why use pw?
In most cases, you should use password-store. Overall, it is much more mature
and feature-rich.

The main difference is that pw.py stores data in a json format, enabling you
to store additional metadata such as username, login page URL, etc:

```
pw github.com update username rpdelaney
```

[1]: https://www.passwordstore.org/

## To-do
* Copy key values to the clipboard (probably using pyperclip)
* Enter a key value at the current cursor position (probably using PyAutoGUI)
