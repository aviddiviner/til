# Rewrite history with `filter-branch`

Start by reading the docs: `git help filter-branch`. Here are some handy example cases.

## Splitting a subfolder out into a new repo

    git filter-branch --prune-empty --subdirectory-filter \
    FOLDER_TO_EXTRACT BRANCH_TO_EXTRACT_FROM

Source: https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/

## Purging files from your repo history

    git filter-branch -f --index-filter \
    "git rm -r --cached --ignore-unmatch PATH_TO_DELETE" \
    --prune-empty --tag-name-filter cat -- --all

Source: https://help.github.com/articles/removing-sensitive-data-from-a-repository/

## Rewriting old commit messages

    git filter-branch -f --msg-filter \
    'sed "s/OLD_COMMIT_MESSAGE/NEW_COMMIT_MESSAGE/g"' \
    --tag-name-filter cat -- --all

### Prepend some text to commit messages

    git filter-branch -f --msg-filter 'sed "s/^/PREPENDED_TEXT/"' master..HEAD
