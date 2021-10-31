Building off of @Gavin's answer:

Making lazygit a function instead of an alias allows you to pass it an argument. I have added the following to my .bashrc (or .bash_profile if Mac):

```bash
function lazygit() {
    git add .
    git commit -a -m "$1"
    git push
}
```
This allows you to provide a commit message, such as  

```bash
lazygit "My commit msg"
```