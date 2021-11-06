You need to write regex that will validate a password to make sure it meets the following criteria:

- At least six characters long
- contains a lowercase letter
- contains an uppercase letter
- contains a number
Valid passwords will only be alphanumeric characters.

```bash
password=$1

# [[ $password =~ (.*[\d]){1,}(.*[\w]){1,}(.*[A-Z]){1,}(.*){6,} ]] && echo "true" || echo "false"

[[  "$password" =~ ^[[:alnum:]]{6,}$ &&
     "$password" =~ [[:upper:]] &&
     "$password" =~ [[:lower:]] &&
     "$password" =~ [[:digit:]] ]] && echo "true" || echo "false"
```