# 4.1.-BASH

## 1.

a+b
1+2
3

## 2. С учетом условия цикл while имеет место быть в течении всего времени, когда сервис недоступен, записывается значение в файл curl.log

while ((1==1))
do
curl https://localhost:4757
if (($? != 0))
  then
    date >> curl.log
  else
    brake  
fi
done

## 3. Необходимо написать скрипт, который проверяет доступность трёх IP: 192.168.0.1, 173.194.222.113, 87.250.250.242 по 80 порту и записывает результат в файл log. Проверять доступность необходимо пять раз для каждого узла.

#!/bin/bash

a=5
b=0
while (($a > 0))
do
  array_out[b]='192.168.0.1:80'
  b+=1
  curl https://192.168.0.1:80
  if (($? != 0))
    then
    echo unavailable >> array_out[b]
    else
    echo available >> array_out[b]
    b+=1
  fi
  
  array_out[b]='173.194.222.113:80'
  b+=1
  curl https://173.194.222.113:80
  if (($? != 0))
   then
    echo unavailable >> array_out[b]
    else
    echo available >> array_out[b]
  b+=1
  fi
  
  array_out[b]='87.250.250.242:80'
  b+=1
  curl https://87.250.250.242:80
  if (($? != 0))
    then
    echo unavailable >> array_out[b]
    else
    echo available >> array_out[b]
  b+=1
  fi
 a-=1
done
echo ${array_out[@]} >> log

## 4.Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается

#!/bin/bash

a=5
b=0
while ((1=1))
do
  array_out[b]='192.168.0.1:80'
  b+=1
  curl https://192.168.0.1:80
  if (($? != 0))
    then
    echo ${array_out[b-1]} >> error
    brake
    else
    echo available >> array_out[b]
    b+=1
  fi
  
  array_out[b]='173.194.222.113:80'
  b+=1
  curl https://173.194.222.113:80
  if (($? != 0))
   then
    echo ${array_out[b-1]} >> error
    brake
    else
    echo available >> array_out[b]
  b+=1
  fi
  
  array_out[b]='87.250.250.242:80'
  b+=1
  curl https://87.250.250.242:80
  if (($? != 0))
    then
    echo ${array_out[b-1]} >> error
    brake
    else
    echo available >> array_out[b]
  b+=1
  fi
 a-=1
done

