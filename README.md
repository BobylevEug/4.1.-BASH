# 4.1.-BASH

## 1.

a=1 b=2 c=a+b d=1+2 e=3

## 2. С учетом условия цикл while имеет место быть в течении всего времени, когда сервис недоступен, записывается значение в файл curl.log

```bash
#! /bin/bash

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
```

## 3. Необходимо написать скрипт, который проверяет доступность трёх IP: 192.168.0.1, 173.194.222.113, 87.250.250.242 по 80 порту и записывает результат в файл log. Проверять доступность необходимо пять раз для каждого узла.

```bash
#! /bin/bash

c=(https://192.168.0.1:80 https://173.194.222.113:80 https://87.250.250.242:80)

cp /dev/null log

for (( a = 0; a < 3; a++ ))
do
  for (( b = 0; b < 5; b++ ))
  do
    if curl ${c[$a]}
      then
      echo ${c[$a]} 'available' >> log
      else
      echo ${c[$a]} 'unavailable' >> log
    fi
  done
done
```

## 4.Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается

```bash
#! /bin/bash

c=(https://192.168.0.1:80 https://173.194.222.113:80 https://87.250.250.242:80)

cp /dev/null log

for (( a = 0; a < 3; a++ ))
do
  for (( b = 0; b < 5; b++ ))
  do
    if curl ${c[$a]}
      then
      echo ${c[$a]} 'available' >> log
      else
      echo ${c[$a]} >> error
      break
    fi
  done
done
```
