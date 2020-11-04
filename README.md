# terminal_misc
experimentos

### ecualizador falso

req: bash, lolcat

req: stty, sed, seq, awk, shuf

```bash
while true; do a="$( seq 1 $( stty -a | sed -nE 's/^.*columns ([0-9]+);.*$/\1/pg' ) | shuf )"; if ! ( [ -z "${a}" ] || [ "$( printf '%s\n' "${a}" | wc -l )" -lt 1 ] ); then i="$( printf '%s' "${a}" | awk -v i=0 -v x="$( printf '%s' "${a}" | sed -n '1p' )" 'BEGIN { i=x } { if ( i > $0 ) { i = $0 }; if ( x < $0 ) { x = $0 }; } END { print i, x; }' )"; x="$( printf '%s' "${i}" | sed 's/^.*\s//' )"; i="$( printf '%s' "${i}" | sed 's/\s.*$//' )"; s=''; for l in $( printf '%s' printf '%s' "${a}" | awk '{ print ( $0 - '"${i}"' ) / ( '"${x}"' - '"${i}"' ); }' | sed -nE 's/[.]//g; s/^(..).*$/\1/pg;' | sed -E 's/^0//' ); do [ ${l} -eq 0  ] && s=" ${s}" || s='\xE2\x96\x'"$(( ${l} + 80 ))${s}"; done; printf "${s}" | lolcat; fi; printf '\r\e[A'; done;
```
