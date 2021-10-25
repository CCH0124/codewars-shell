
Your task in order to complete this Kata is to write a function which formats a duration, given as a number of seconds, in a human-friendly way.


The function must accept a non-negative integer. If it is zero, it just returns `"now"`. Otherwise, the duration is expressed as a combination of `years`, `days`, `hours`, `minutes` and `seconds`.

It is much easier to understand with an example:

```
duration 62            # echos "1 minute and 2 seconds"
duration 3662          # echos "1 hour, 1 minute and 2 seconds"
```
**For the purpose of this Kata, a year is 365 days and a day is 24 hours.**

Note that spaces are important.

## Detailed rules

The resulting expression is made of components like `4 seconds`, `1 year`, etc. In general, a positive integer and one of the valid units of time, separated by a space. The unit of time is used in plural if the integer is greater than 1.

The components are separated by a comma and a space `(", ")`. Except the last component, which is separated by `" and "`, just like it would be written in English.

A more significant units of time will occur before than a least significant one. Therefore, `1 second and 1 year` is not correct, but `1 year and 1 second` is.

Different components have different unit of times. So there is not repeated units like in `5 seconds and 1 second`.

A component will not appear at all if its value happens to be zero. Hence, `1 minute and 0 seconds` is not valid, but it should be just `1 minute`.

A unit of time must be used "as much as possible". It means that the function should not return `61 seconds`, but `1 minute and 1 second` instead. Formally, the duration specified by of a component must not be greater than any valid more significant unit of time.


```bash
#!/bin/bash
function duration() {
  if [[ $1 -eq 0 ]]; then
        echo "now"
        exit
  fi
  let seconds=$1
  let years=0
  let days=0
  let hour=0
  let min=0
  let sec=0
 
  sec=$((seconds%60))
  min=$(((seconds/60)%60))
  hour=$(((seconds/60/60)%24))
  days=$(((seconds/60/60/24)%365))
  years=$(((seconds/60/60/24/365)))
  
  delim=()
  item=()
  [[ $years != 0 ]] && delim+=($years) && item+=("year")
  [[ $days != 0 ]] && delim+=("$days") && item+=("day")
  [[ $hour != 0 ]] && delim+=("$hour") && item+=("hour")
  [[ $min != 0 ]] && delim+=("$min") && item+=("minute")
  [[ $sec != 0 ]] && delim+=("$sec") && item+=("second")

  delim_len=${#delim[@]}
  len=0
  for i in "${delim[@]}";
  do
    if [ $i -ne 0 ]; then
      res=$res$i" ${item[$len]}"
      if [ $i -gt 1 ]; then
        res=$res"s"
      fi
      if [ $(($delim_len - $len)) -gt 2 ];
      then
        res=$res", "
      fi
      if [ $(($delim_len - $len)) -eq 2 ];
      then
        res=$res" and "
      fi
    fi
    len=$((len+1))
  done
  echo $res
}
duration "$1"
```