Write a function, which takes a non-negative integer (seconds) as input and returns the time in a human-readable format (`HH:MM:SS`)

`HH` = hours, padded to 2 digits, range: 00 - 99
`MM` = minutes, padded to 2 digits, range: 00 - 59
`SS` = seconds, padded to 2 digits, range: 00 - 59
The maximum time never exceeds 359999 (`99:59:59`)

You can find some examples in the test fixtures.

```shell
#!/bin/bash

seconds=$1
# Do something
sec=$((seconds%60))
min=$(((seconds/60)%60))
hour=$((seconds/60/60))

if [ $sec -lt  10 ];
then
  sec=0$sec
fi

if [ $min -lt 10 ];
then
  min=0$min
fi

if [ $hour -lt 10 ];
then
  hour=0$hour
fi

seconds=$hour:$min:$sec
echo $seconds
```