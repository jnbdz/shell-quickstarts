# Spinner
The two spinners do the same thing. But one is POSIX.

## Slowing it down
In the while loop you can add the `sleep` command after the `printf`.

## Integration
```bash
sp="/-\|"
sc=0
spin() {
   printf "\b${sp:sc++:1}"
   ((sc==${#sp})) && sc=0
}
endspin() {
   printf "\r%s\n" "$@"
}

until work_done; do
   spin
   some_work ...
done
endspin
```

## Details
Each loop it iterates to the next character in `sp` string.

`i` variable is the position in the loop.

`${#sp}` gets you the length.

`\b` is replace by a *backspace* character.

You could use the `\r` to go back to the beginning of the line.

**Source:** https://stackoverflow.com/questions/238073/how-to-add-a-progress-bar-to-a-shell-script (one of the answers)
