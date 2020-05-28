# Shell Cheat Sheets


## References

- [Bash reference manual](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#index-trap-125)
- [Cheat sheet](https://gist.github.com/LeCoupa/122b12050f5fb267e75f)
- [Google style convention](https://google.github.io/styleguide/shellguide.html)

## Bourne shell

Bourne shell is sensitive to round brackets `()`. For example:

```bash
# /bin/sh
(echo "1.2.3" | grep -Eq ^[0-9]+\.[0-9]+\.[0-9]+$ && VAL=0) || VAL=1;
echo $VAL; # ''
echo "1.2.3" | grep -Eq ^[0-9]+\.[0-9]+\.[0-9]+$ && VAL=0 || VAL=1;
echo $VAL; # 0

# /bin/bash
(echo "1.2.3" | grep -Eq ^[0-9]+\.[0-9]+\.[0-9]+$ && VAL="OK") || VAL="NOK"
echo $VAL # OK
```

Double quotes in Bourne shell make strings un-loopable:

```bash
#!/bin/bash
# Read a string with spaces using for loop
for value in I like programming
do
    echo $value;
done

val="I like programming";
for value in $val
do
    echo $value;
done

# I
# like
# programming

for value in "$val"
do
    echo $value;
done

# I like programming
```

Attention, `IFS` can change the default behavior, for example, `IFS=""` will not split strings by space. The output value will be `I like programming`.

## Shell scripting

Exit when any commands return a non-zero exit code:

```shell
# exit when any command fails
set -e
```

Further advanced exit strategies are available [here](https://intoli.com/blog/exit-on-errors-in-bash-scripts/)

## Troubleshooting

### Return values in functions

Bash can't pass around data structures as return values in functions. A return value must be a numeric exit status between 0-255. It's not recommended to return structured data like below:

```shell
# Don't
get_users() {
    user=(John Dave Amy)
    echo "${user[@]}"
}

give_gifts() {
    local users=$(get_users)

    for user in "${users[@]}"
    do
        echo "Give ${user} a gift"
    done
}
```

With Bash version 4.3 and above, we can make use of a nameref to pass return data.

```shell
# Do
get_userz() {
    local -n arr=$1 # use nameref for indirection
    arr=(John Dave Amy)
}

give_gifts() {
    local userz
    get_userz userz

    for user in "${users[@]}"
    do
        echo "Give ${user} a gift"
    done
}
```

### gitlab-ci.yml

YAML files used in GitLab CI does not support colon (:) in commands, i.e. `curl -H "access-token: test"`. Use with care.
