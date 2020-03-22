# modified pageant

This fork exists because I needed a slightly modified version of PuTTY's `pageant.exe` for a special use case.

## What it does

If you use `pageant.exe` with the `-c` option to have it run a command after it processed the key, you'll notice that the command is executed regardless of the key being successfully added or not. For example, if the key is password protected and you cancel the password prompt, the key is not added but the command will still be executed. If that command requires that key, it'll run into an error.

This modified version of `pageant.exe` will append an extra argument to the command that indicates success (argument will be the number `0`) or failure (argument will be the number of failures, e.g. with one key it'll be `1`).

### Example

1. Create a password protected key `mykey.ppk`.

2. Run the following command

   ```bat
   pageant.exe mykey.ppk -c cmd.exe /K echo hello
   ```

   and cancel the password dialog. A new window will open and show the message

   ```text
   hello 1
   ```

3. Run the above command again, but enter the correct password this time. A new window will open and show the message

   ```text
   hello 0
   ```

## License

See the original [LICENCE](LICENCE) file.
