#### If you have Nvidia graphic card that demand proprietary drivers and Ubuntu installation failed

Сам с такой проблемой столкнулся , когда купил ноут с Nvidia. 

1) В GRUB menu жмем 'e'
2) добовляем nomodeset перед $vt_handoff
3) В DriverManager ставим оффициальные драйвера для Nvidia

Тут подробная инструкция 
https://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it

Тут установка драйвера 
https://askubuntu.com/questions/47506/how-do-i-install-additional-drivers

#### first commands on new OS Ubuntu

- whoami
- sudo apt-get update
- sudo apt-get install aptitude
- sudo aptitude safe-upgrade

### working with hardware on Ubuntu

- hwinfo --short

#### Processor utilization

![](https://github.com/IgorSondors/cheatsheet/blob/master/images/2.jpg)

![](https://github.com/IgorSondors/cheatsheet/blob/master/images/3.jpg)

#### Check RAM

- sudo lshw -C memory

### Ssh connection

#### Files transfer

#### Вводить на локальной машине 
#### для переноса с локальной на удаленную

- scp -r /home/sondors/Recognizer/cloud_server/neurohives root@138.68.65.54:~/cloud_server/neurohives

#### для переноса с удаленной на локальную

- sudo scp -r root@138.68.65.54:/~/cloud_server/neurohives  /home/sondors/Recognizer/cloud_server/neurohives
