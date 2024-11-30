`
a=$1
b=$2
if [[ "$a" -gt 0 ]] && [[ "$b" -gt 0 ]];then
        echo "$((a + b))"
else
        echo "NOT INTEGERS" >&2
        exit 1
fi
`
`
a=$1
b=$2
if [[ "$a" =~ ^[0-9]+$ ]] && [[ "$b" =~ ^[0-9]+$ ]];then
        echo "$((a + b))"
else
        echo "NOT INTEGERS" >&2
        exit 1
fi

`
