# Progress Bar
A simple Bash progress bar without `\n` line return.

## Some details
The flags `-ne` for `echo` is for priting without `\n` and `\r`.

## progressBar3
Based on: https://github.com/edouard-lopez/progress-bar.sh

But for some reason it doesn't work at all on debian/Kali Linux.

## Implementing it with `cp`
```bash
#!/bin/sh

src="/path/to/source/file"
tgt="/path/to/target/file"

cp "$src" "$tgt" &                     # the & forks the `cp` process so the rest
                                       # of the code runs without waiting (async)

BAR='####################'

src_size=$(stat -c%s "$src")           # how much there is to do

while true; do
    tgt_size=$(stat -c%s "$tgt")       # how much has been done so far
    i=$(( $tgt_size * 20 / $src_size ))
    echo -ne "\r${BAR:0:$i}"
    if [ $tgt_size == $src_size ]; then
        echo ""                        # add a new line at the end
        break;                         # break the loop
    fi
    sleep .1
done
```

**Source:** 
- https://stackoverflow.com/questions/238073/how-to-add-a-progress-bar-to-a-shell-script
- https://github.com/fearside/ProgressBar/ (for the `progressBar2`)
