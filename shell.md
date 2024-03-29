## `mc` commands and shortcuts
> Copied from: http://pastebin.com/i9kfVKT9

### Esc
Quick change directory: `Esc + c`

Quick change directory history: `Esc + c` and then `Esc + h`

Quick change directory previous entry: `Esc + c` and then `Esc + p`

Command line history: `Esc + h`

Command line previous command: `Esc + p`

View change: `Esc + t` (each time you do this shortcut a new directory view will appear)

Print current working directory in command line: `Esc + a`

Switch between background command line and MC: `Ctrl + o`

Search/Go to directory in active panel: `Esc + s` / `Ctrl + s` then start typing directory name

Open same working directory in the inactive panel: `Esc + i`

Open parent working directory in the inactive panel: `Esc + o`

Go to top of directory in active pane: `Esc + v` / `Esc + g`

Go to bottom of directory in active pane: `Esc + j` / `Ctrl + c`

Go to previous directory: `Esc + y`

Search pop-up: `Esc + ?`

### Ctrl
Refresh active panel: `Ctrl + r`

Selecting files and directories: `Ctrl + t`

Switch active <-> inactive panels: `Ctrl + i`

Switch active <-> inactive panels content: `Ctrl + u`

Execute command / Open a directory: `Ctrl + j`

## Right way to check DNS for a host in macOS

`dscacheutil -q host -a name www.foobar.dev`

## Save code repo to Word document

```bash
find . -type f > files.txt
mkdir htmls
n=0; while read line; do echo "<h3>$line<h3>" > htmls/$n.html; cat $line | ansi2html -t $line | tee -a htmls/$n.html; n=$((n+1)); done < files.txt
cat htmls/* | pandoc -f html -t docx -o general.docx
```
