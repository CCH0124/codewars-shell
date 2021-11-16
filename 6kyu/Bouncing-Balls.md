His mother looks out of a window 1.5 meters from the ground.

How many times will the mother see the ball pass in front of her window (including when it's falling and bouncing?

Three conditions must be met for a valid experiment:
- Float parameter "h" in meters must be greater than 0
- Float parameter "bounce" must be greater than 0 and less than 1
- Float parameter "window" must be less than h.

If all three conditions above are fulfilled, return a positive integer, otherwise return -1.

**Note:**

The ball can only be seen if the height of the rebounding ball is strictly greater than the window parameter.

**Examples:**
```
- h = 3, bounce = 0.66, window = 1.5, result is 3

- h = 3, bounce = 1, window = 1.5, result is -1 

(Condition 2) not fulfilled).
```

```bash
#!/bin/bash
bouncingBall() {
    # your code
    local res=-1
    if [  $( echo "$1 > 0" | bc ) -eq 0 -o $( echo "$3 < $1" | bc -l ) -eq 0 -o  $( echo "$2 < 1 && $2 > 0" | bc ) -eq 0 ];
    then
      echo $res
      exit
    fi
    local h=$1
    local w=$3
    while [ $( echo "$h > $w " | bc ) -eq 1 ]; do
      res=$(($res+2))
      h=$( echo "scale=8; $h * $2" | bc )
    done
    
    echo $res
    
}
bouncingBall $1 $2 $3
```

關於 double 符號比較參考 https://stackoverflow.com/questions/8654051/how-can-i-compare-two-floating-point-numbers-in-bash