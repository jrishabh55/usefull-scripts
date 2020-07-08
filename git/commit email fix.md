A quick script for helping mutate/fix commit email address if config was incorrect accidently. 

```sh
#!/bin/sh

git filter-branch --env-filter '
OLD_EMAIL="rishbah@codeation.io"
CORRECT_NAME="Rishabh Jain"
CORRECT_EMAIL="rishabh@codeation.io"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
