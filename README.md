# terminal_misc
experimentos en la terminal, todo listo para copy+paste, ver **req** por detalles

### ecualizador falso

req: lolcat, bash, stty, sed, seq, awk, shuf

```bash
while true;do a="$(seq 1 $(stty -a|sed -nE 's/^.*columns ([0-9]+);.*$/\1/pg')|shuf)";i="$(printf '%s' "${a}"|awk -v i=0 -v x="$(printf '%s' "${a}"|sed -n '1p')" 'BEGIN{i=x}{if(i>$0){i=$0};if(x<$0){x=$0}}END{print i, x;}')";x="$(printf '%s' "${i}"|sed 's/^.*\s//')";i="$(printf '%s' "${i}"|sed 's/\s.*$//')";s='';for l in $(printf "${a}"|awk '{print ($0-'"${i}"')/('"${x}"'-'"${i}"')}'|sed -nE 's/[.]//g;s/^(..).*$/\1/pg'|sed -E 's/^0//');do [ ${l} -eq 0 ]&&s=" ${s}"|| s='\xE2\x96\x'"$((${l}+80))${s}";done;printf "${s}"|lolcat;printf '\r\e[A';done;
```
