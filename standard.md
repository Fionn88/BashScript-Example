# programs

## && Practice
> cat `love.sh`
```
#!/bin/bash
read -p 'Do you love me?(Y/N)' ans
[ ${ans,,} = "y" ] && echo 'I love yot,too.'
[ ${ans,,} = "n" ] && echo 'I hate you.'
```

## Search Folder & If Not Build It

> cat `mkd.sh`
```
#!/bin/bash
read -p 'input your dirctory: ' ans
[ -d $ans ] && echo 'You already have!'
[ ! -d $ans ] && mkdir $ans && echo 'You have new one.'
```

## Search File & If Not Build It
> cat `mkf.sh`
```
#!/bin/bash
read -p 'input your file: ' ans
[ -f $ans ] && echo 'You already have!'
[ ! -f $ans ] && touch $ans && echo 'You hava new one.'
```

## If Else Practice
> cat `loveif.sh`
```
#!/bin/bash
echo "Do you love me(Y/N)?"
read ans
if [ "$ans" = "y" ] || [ "$ans" = "Y" ]
then
 echo "I love you,too!"
else
 echo "I hate you."
fi
echo "END"
```

> cat `point.sh`
```
#!/bin/bash
read -p 'Input Your Point: ' ans
if
[ ${ans} -le 60 ]
then
echo "D grade"
elif
[ ${ans} -gt 60 ] && [ ${ans} -le 80 ]
then
echo "C grade"
elif
[ ${ans} -gt 80 ] && [ ${ans} -le 90 ]
then
echo "B grade"
elif
[ ${ans} -gt 90 ] && [ ${ans} -le 98 ]
then
echo "A grade"
elif
[ ${ans} -ge 99 ] && [ ${ans} -le 100 ]
then
echo "A+ grade"
fi
```

## Filter Characters
- Filter a-z A-z 8 0 Change Null Value
> cat `pass.sh`
```
#!/bin/bash
read  -p "password?" ans
[ ${ans//[a-zA-Z80]/} = "12345" ] && echo "pass"
```
- All Capital Characters Change Lower Case
> cat `pass01.sh`
```
#!/bin/bash
echo 'Password Or Die!!'
read ans
if
[ ${ans,,} == 'qwer' ]
then
echo "You will die comfortable"
else
echo "You Die!!!!!!!!"
fi
```

## For Loop Practice
> cat `wait.sh`
```
#!/bin/bash
for load in $(seq 1 100); do
    echo -ne "$load \r"
    sleep 1
done
```

- accumulation
> cat `mycal.sh`
```
#!/bin/bash
t=0
for x in $@
do
  t=$(($t+$x))
done
echo $t
```

## Case Practice
> cat `case.sh`
```
#!/bin/bash
read -p "Do you like Trump?(y/n) " number
case ${number,,} in
y)
  echo "Trump fans + 1"
  ;;
n)
  echo "Trump hater + 1"
  ;;
*)
  echo "Please entry(y or n)?"
  ;;
esac
echo "Thanks your apply"
```

> cat `case01.sh`
```
#!/bin/bash
read -p 'input your number(1-4): ' ans
case $ans in
1)
   echo "you chose 1"
   ;;
2)
   echo "you chose 2"
   ;;
3)
   echo "you chose 3"
   ;;
4)
   echo "you chose 4"
   ;;
*)
   echo "Please chose 1 to 4"
esac
echo "Thanks"
```

## While Loop & Case Practice
> cat `while.sh`
```
#!/bin/bash
while :
do
read -p 'Do you like Trump?(y/n)' ans
case ${ans,,} in
y)
  echo "Trump fans +1"
  break
  ;;
n)
  echo "Trump hater +1"
  break
  ;;
*)
  echo "Please answer y or n"
esac
done
echo "Thanks"
```

## Show Last Five User
> cat `user.sh`
```
#!/bin/bash
user=$(cat /etc/passwd | tail -n 5 | fmt -u | cut -d':' -f1)
echo -e " users:
$user"
```

## Change Address,Subnet Mask,Gateway & Show After Change
> cat `changeip.sh`
```
#!/bin/bash
read -p "input your ip: " addr
read -p "input your netmask: " net
read -p "input your defalt gateway: " way
sudo ifconfig ens33 $addr netmask $net
sudo route add default gw $way

gateway2=$(route -n | tail -n +3 | fmt -u | cut -d' ' -f 2 | head -n 1)
echo "gateway: '$gateway2'"
dns=$(cat /etc/resolv.conf | grep 'nameserver' | fmt -u | cut -d' ' -f2)
echo "DNS: '$dns'"
netmask2=$(ifconfig | grep 'netmask' | fmt -u | head -n 1 | tr -s ' ' | cut -d' ' -f 5)
echo "subnetmask: '$netmask2'"
ip2=$(ifconfig | grep 'inet' | fmt -u | head -n 1 | tr -s ' ' | cut -d' ' -f 3)
echo "IP: '$ip2'"
```

## Ping Avaliable
> cat `ping.sh`
```
#!/bin/bash
read -p 'input ip: ' ans
ping -c 1 $ans > /dev/null
if
[ "$?" == "0" ]
then
echo "$ans avaliable"
else
echo "$ans unavaliable"
fi
```

> cat `pingping.sh`
```
#!/bin/bash
read -p 'Enter Start Value: ' start
read -p 'Enter End Value: ' end
for ((no=${start};no<=${end};no=no+1))
do
for ((ip=0;ip<=255;ip++))
do
ping -w 1 192.168.$no.$ip > /dev/null
if
[ "$?" == "0" ]
then
echo "192.168.$no.$ip avaliable"
else
echo "192.168.$no.$ip unavaliable"
fi
done
done
```

## Source Practice
> cat `allfun`
```
function add(){
read -p 'Enter First: ' ans
read -p 'Enter Second: ' ans1

t=$((ans+ans1))
echo $t
}

function sub(){
read -p 'Enter First: ' ans
read -p 'Enter Second: ' ans1

t=$((ans-ans1))
echo $t
}

function multi(){
read -p 'Enter First: ' ans
read -p 'Enter Second: ' ans1

t=$((ans*ans1))
echo $t
}

function divi(){
read -p 'Enter First: ' ans
read -p 'Enter Second: ' ans1

t=$((ans/ans1))
echo $t
}
```

> cat `source.sh`
```
#!/bin/bash
source allfun
select var in "+" "-" "*" "/" "Exit"
do
case $REPLY in
1)
  add
  ;;
2)
  sub
  ;;
3)
  multi
  ;;
4)
  divi
  ;;
5)
  break
  ;;
*)
  echo 'Please Select 1,2,3,4,5'
esac
done

```
## Account System
> cat `main_computer.sh`
```
#!/bin/bash
while :
do
echo '
        Menu
     1. Search Account
     2. Creat Account
     3. Delete Accout
     4. Update Password
     5. Sudo Chmod
     6. Exit
'
read -p 'Please select 1,2,3,4,5,6: ' ans
case ${ans} in
1)
  ./search.sh
  ;;
2)
  ./create.sh
  ;;
3)
  ./main_delete.sh
  ;;
4)
  ./main_update.sh
  ;;
5)
  ./main_sudo.sh
  ;;
6)
  break
  ;;
*)
  echo "Please Select 1,2,3,4,5,6"
  ;;
esac
done
echo "Thanks"
```

### Search Account
> cat `search.sh`
```
#!/bin/bash
read -p 'What do you want to Search: ' ans
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans)
if [ ! -n "$account" ]
then
  echo "Account doesn't exist"
else
  echo "Account already exist"
fi
```

### Creat Account
> cat `create.sh`
```
#!/bin/bash
echo '
       Menu
     1. Create a account
     2. Create a series account
     3. Exit
'
while :
do
read -p 'Please Select 1,2,3: ' ans
case ${ans} in
1)
  ./account.sh
  break
  ;;
2)
  ./accounts.sh
  break
  ;;
3)
  break
  ;;
*)
  echo "Please Select 1,2,3"
esac
done
echo "Thanks"
```

#### Create a account
> cat `account.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p 'Give me a name: ' ans
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans)
if [ ! -n "$account" ]
then
  sudo useradd -m -s /bin/bash $ans
  echo "${ans}:${ans}" > passwd.txt
  sudo chpasswd < passwd.txt
  echo "$ans Account Create!!"
else
  echo "$ans Account already exist"
fi
fi
```
#### Create a series account
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p "Enter head name To Create: " ans
read -p "Enter Start value To Create: " start
read -p "Enter End Value To Create: " end
 for ((no=${start};no<=${end};no=no+1))
do
  account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans$no)
  if [ ! -n "$account" ]
  then
    sudo useradd -m -s /bin/bash $ans$no
    echo "$ans$no:$ans$no" > passwd.txt
    sudo chpasswd < passwd.txt
    echo "Create $ans$no !!"
  else
    echo "$ans$no Account already exist"
  fi
done
fi
```


### Delete Accout
> cat `main_delete.sh`
```
#!/bin/bash
echo '
     Menu
   1. Delete a Account
   2. Delete a series Account
   3. Exit
'
while :
do
read -p 'Please Select 1,2,3: ' ans
case $ans in
1)
  ./delete.sh
  break
  ;;
2)
  ./deletes.sh
  break
  ;;
3)
  break
  ;;
*)
  echo 'Please Select 1,2,3'
esac
done
echo 'Thanks'
```

#### Delete A Account
> cat `delete.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p 'What do you want to delete: ' ans
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans)
if [ ! -n "$account" ]
  then
    echo "$ans Account doesn't exist"
  else
    sudo userdel -r $ans
    echo "$ans delete!!"
 fi
fi
```

#### Delete A Series Account
> cat `deletes.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p "Enter Head Name To Delete: " ans
read -p "Enter Start value To Delete: " start
read -p "Enter End Value To Delete: " end
 for ((no=${start};no<=${end};no=no+1))
do
  account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans$no)
  if [ ! -n "$account" ]
  then
    echo "$ans$no Account doesn't exist"
  else
    sudo userdel -r $ans$no
    echo "$ans$no delete!!"
fi
done
fi
```


### Update Account
> cat `main_update.sh`
```
#!/bin/bash
echo '
      Menu
    1. Update A Account
    2. Update A Series Account
    3. Exit
'
while :
do
read -p 'Please Select 1,2,3: ' ans
case $ans in
1)
  ./update.sh
  break
  ;;
2)
  ./updates.sh
  break
  ;;
3)
  break
  ;;
*)
  echo "Please Select 1,2,3"
  ;;
esac
done
echo "Thanks"
```

#### Update A Account
> cat `update.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p 'Which User Do You Want To Update Passwd: ' ans
read -p 'New Passwd: ' ans1
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans)
if [ ! -n "$account" ]
  then
    echo "$ans Account doesn't exist"
  else
    echo "${ans}:${ans1}" > passwd.txt
    sudo chpasswd < passwd.txt
    echo "$ans Account Update!!"
fi
fi
```

#### Update A Series Account
> cat `updates.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p "Enter Head Name To Update: " ans
read -p "Enter Start Value To Update: " start
read -p "Enter End Value To Update: " end
read -p "Enter All New Passwd: " ans1
 for ((no=${start};no<=${end};no=no+1))
do
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans$no)
if [ ! -n "$account" ]
  then
    echo "$ans$no Account doesn't exist"
  else
    echo "$ans$no:$ans1" > passwd.txt
    sudo chpasswd < passwd.txt
    echo "$ans$no Account Update!!"
fi
done
fi
```

### Edit Permissions
> cat `main_sudo.sh`
```
#!/bin/bash
echo '
        Menu
    1. Chmod A Account
    2. Chmod A Sereis Account
    3. Exit
'
while :
do
read -p 'Please Select 1,2,3: ' ans
case $ans in
1)
  ./chmodsudo.sh
  break
  ;;
2)
  ./chmodsudos.sh
  break
  ;;
3)
  break
  ;;
*)
  echo 'Please Select 1,2,3'
  ;;
esac
done
echo 'Thanks'
```

#### Chmod A Account
> cat `chmodsudo.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p 'What User Do You Want To Change Root: ' ans
account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans)
if [ ! -n "$account" ]
then
  echo "$ans Account Doesn't Exist"
else
  sudo usermod -aG sudo $ans
  echo "$ans Is A Root!"
fi
fi
```

#### Chmod A Sereis Account
> cat `chmodsudos.sh`
```
#!/bin/bash
check=$(sudo -l | head -n 1 | fmt -u | cut -d' ' -f1)
if [ $check != 'Matching' ]
then
echo 'You Do Not A Root!'
else
read -p "Enter head name To Chmod: " ans
read -p "Enter Start value To Chmod: " start
read -p "Enter End Value To Chmod: " end
 for ((no=${start};no<=${end};no=no+1))
do
  account=$(cat /etc/passwd | cut -d ':' -f1 | grep -x $ans$no)
  if [ ! -n "$account" ]
  then
    echo "$ans$no Account Doesn't Exist"
  else
    sudo usermod -aG sudo $ans$no
    echo "$ans$no Chmod!"
  fi
done
fi
```

## Compter Information System
> cat `main_tools.sh`
```
#!/bin/bash
while :
do
echo '
     Menu
   1. System Infoemaiton
   2. Network Information
   3. BusyBox Web
   4. Exit
'
read -p 'Please Select 1,2,3,4: ' ans
case ${ans} in
1)
  ./main_system.sh
  ;;
2)
  ./main_net.sh
  ;;
3)
  ./main_network.sh
4)
  break
  ;;
*)
  echo "Please Select 1,2,3,4"
  ;;
esac
done
echo 'Thanks'
```

### System Infoemaiton
> cat `main_system.sh`
```
#!/bin/bash
echo '
       Menu
      1. hostname
      2. computer bit
      3. RAM
      4. Disk
      5. CPU
      6. Linux Standard
      7. Exit'
while :
do
read -p 'Please Select 1,2,3,4,5,6,7: ' ans
case $ans in
1)
  hostname=$(cat /etc/hostname)
  echo "hostname: '$hostname'"
  ;;
2)
  bit=$(hostnamectl | fmt -u | grep 'Architecture' | cut -d':' -f 2)
  echo "computer bit: '$bit'"
  ;;
3)
  memo=$( free -mh | grep Mem: | fmt -u | cut -d' ' -f2 )
  echo "RAM: '$memo'"
  ;;
4)
  disk=$( df -h | grep '/dev/sda' | fmt -u | cut -d' ' -f2 )
  echo "sda: '$disk'"
  ;;
5)
  cpu=$( cat /proc/cpuinfo | grep 'model name' | head -n 1 | fmt -u | cut -d':' -f2 )
  echo "cpu: '$cpu'"
  ;;
6)
  operating=$(uname -m)
  echo "Operating System: '$operating'"
  version=$(cat /etc/issue.net)
  echo "Version: '$version'"
  ;;
7)
  break
  ;;
*)
  echo "Please Select 1-7"
esac
done
echo 'Thanks'
```

### Network Information
> cat `main_net.sh`
```
#!/bin/bash
while :
do
echo '
      Menu
    1. IP
    2. netmask
    3. gateway
    4. DNS
    5. Search IP avaliable
    6. insatll tree,openssh,busybox,net-tools,nmap
    7. Exit
'
read -p 'Please Select 1,2,3,4,5,6,7: ' ans
case $ans in
1)
  ip2=$(ifconfig | grep 'inet' | fmt -u | head -n 1 | tr -s ' ' | cut -d' ' -f3)
  echo "IP: '$ip2'"
  ;;
2)
  netmask2=$(ifconfig | grep 'netmask' | fmt -u | head -n 1 | tr -s ' ' | cut -d' ' -f 5)
  echo "subnetmask: '$netmask2'"
  ;;
3)
  gateway2=$(route -n | tail -n +3 | fmt -u | cut -d' ' -f 2 | head -n 1)
  echo "gateway: '$gateway2'"
  ;;
4)
  dns=$(cat /etc/resolv.conf | grep 'nameserver' | fmt -u | cut -d' ' -f2)
  echo "DNS: '$dns'"
  ;;
5)
  read -p 'Enter Start Value: ' start
  read -p 'Enter End Value: ' end
  for ((no=${start};no<=${end};no=no+1))
  do
  for ((ip=0;ip<=255;ip++))
  do
  ping -w 1 192.168.$no.$ip > /dev/null
  if
  [ "$?" == "0" ]
  then
  echo "192.168.$no.$ip avaliable"
  else
  echo "192.168.$no.$ip unavaliable"
  fi
  done
  done
  ;;
6)
  sudo apt -y update &> /dev/null
  sudo apt -y upgrade &> /dev/null
  sudo apt -y install tree &> /dev/null
  if [ $? == 0 ]
  then
  echo "Install Tree"
  fi
  sudo apt -y install openssh-server &> /dev/null
  if [ $? == 0 ]
  then
  echo "Install openssh-server"
  fi
  sudo apt -y install net-tools &> /dev/null
  if [ $? == 0 ]
  then
  echo "Install net-tools"
  fi
  sudo apt -y install nmap &> /dev/null
  if [ $? == 0 ]
  then
  echo "Install openssh-server"
  fi
  sudo apt -y install elinks &> /dev/null
  if [ $? == 0 ]
  then
  echo "Install elinks"
  fi
  wget 'https://busybox.net/downloads/binaries/1.28.1-defconfig-multiarch/busybox-x86_64'
  chmod +x busybox-x86_64
  mkdir web
  mv busybox-x86_64 web/busybox
  mkdir dataset
  echo '<h1>Let Me Go</h1>' > dataset/index.html
  ;;
7)
  break
  ;;
*)
  echo 'Please Select 1,2,3,4,5,6,7'

esac
done
echo 'Thanks'
```
### BusyBox Web
> cat `main_network.sh`
```
#!/bin/bash
select cho in OpenNetWork ShowPage CloseNetWork Exit
do
case $cho in
"OpenNetWork")
   busybox httpd -p 8888 -h dataset
   echo "Open"
   ;;
"ShowPage")
  elinks -dump 1 http://localhost:8888
  ;;

"CloseNetWork")
  pass=$(ps aux | tr -s ' ' | grep 'busybox' | cut -d' ' -f2 | head -n 1)
  kill -9 $pass
  ;;
"Exit")
  exit
  ;;
*)
  echo "Please Select 1,2,3,4"
  ;;
esac
done
```