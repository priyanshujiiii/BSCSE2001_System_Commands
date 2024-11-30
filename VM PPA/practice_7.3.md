a=$1
b=$2
if [[ "$a" =~ ^[0-9]+$ ]] && [[ "$b" =~ ^[0-9]+$ ]];then
        echo "$((a + b))"
else
        echo "$a$b"
fi
