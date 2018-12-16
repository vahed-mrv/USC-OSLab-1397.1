# Lesson3

## Bash Script

### printf
```
printf "%s : %d" Ali 14
printf "%10s" sample
printf "%.2f" 13.2345
```

### Variables
```
var1=123
name=mohammad
printf "%s : %d" $name $var1
```
- Don't use space
- Case sensitive

### Enviornment Variables
- در این اسکریپت و بچه هایش ولید است.

```
export var2=sag
```

### Math Calculation
```
echo $[$num1+$num2]
echo $[2+4]

echo $(($num1+$NUM2))

let num3=$num1+$num2
echo $num3
```
- `$num1+$num2` is concatination

### Exit
```
exit

exit 0
```
- `$?` is exit value
```
./script.sh && echo 'true' || echo 'false' #if script return 0 then write true, else write false
```

### Conditions

#### Test
```
[ 2 = 1 ]

[ 2 = 1 ] && echo 'true' || echo 'false'

[ $var1 = $var2 ] && echo 'true' || echo 'false'
[ $var1 != $var2 ] && echo 'true' || echo 'false'
```

```
var1=12
var2=12

[ $var1 -gt $var2 ] #greater than
[ $var1 -lt $var2 ] #lower than
[ $var1 -ge $var2 ] #greater equal
[ $var1 -gt $var2 ] #lower equal

[ $var1 -ne $var2 -a $var1 -ge $var2 ] # not equal | and | greater equal

str1=ali
[ -n $str1 ] # non-zero
```
- `man test` is usefull
- diffrent for `integer` and `string`

#### if
```
if [ $var1 -eq $var2 ]
then
	echo 'equal'
else
	echo 'not equal'
fi
```
- we can use `elif-then` statement

#### case
```
case $num4 in
	20)
		echo '20';;
	21)
		echo '21';;
	23|24)
		echo '23 or 24';;
	*) #default
		echo 'else';;
esac
```
- `;;` is break