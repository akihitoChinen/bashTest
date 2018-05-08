# bashTest

#!/bin/sh
#javacの実行
javac $1
if [ $? = 1 ]; then
  exit 1
fi

#引数のファイルを一行ずつ読み込み、class名を含む行を探す
#classNameLine=""
while read line
do
  echo $line | grep "class" > /dev/null
  if [ $? = 0 ]; then
    classNameLine=$line
    break
  fi
done < $1

#得られた一行からclass名のみを分割・抽出
#echo $classNameLine
split=( `echo $classNameLine | tr -s ',{' ' '`)
argument=${split[1]}
java $argument
