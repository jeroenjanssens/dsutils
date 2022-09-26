#!/usr/bin/env bash
#
# NAME
#       trim -- trim output to a given height and width.
#
# USAGE
#       trim [height] [width]
#
#       By default, output is trimmed to 10 lines and the width of the terminal.
#       Pass a negative number to disable trimming the height and or width. 
#       Before trimming, tabs are expanded to spaces.
#
# EXAMPLES
#       seq 100 | trim
#       seq 100 | trim 20 
#       seq 100 | trim 20 40
#       seq 100 | trim -1 40
#       seq 100 | trim 20 -1
#
# Author: Jeroen Janssens (https://jeroenjanssens.com)
#
# LICENSE: MIT (2021)

set -euf -o pipefail

HEIGHT="${1:-10}"
WIDTH="${2:-$(tput cols)}"

expand |
awk -v height="${HEIGHT}" -v width="${WIDTH}" \
'function tprint() {
    if (width > 0 && length($0) > width) {
        print substr($0, 1, width - 1) "…"
    } else {
        print
    }
}

height <= 0 || NR <= height {
    tprint()
}

END {
    if (height > 0) {
        if (NR == height + 1) {
            tprint()
        } else if (NR > height + 1) {
            print "… with " (NR - height) " more lines"
        }
    }
}'
