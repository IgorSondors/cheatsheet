### Dohod

#### Commands for work with server

- ssh sondors@192.168.128.44
- Dom72Kpa5
- cd /opt/cloud_server/

#### Control version system

- merge code [there](http://code.dohod.local/AI/cloud_server)
- login: iso
- password_new: Kap17Dom9


#### If you have Nvidia GPU that demand proprietary drivers and Ubuntu installation failed

Сам с такой проблемой столкнулся , когда купил ноут с Nvidia. 

1) В GRUB menu жмем 'e'
2) добовляем nomodeset перед $vt_handoff
3) В DriverManager ставим оффициальные драйвера для Nvidia

Тут подробная инструкция 
https://askubuntu.com/questions/162075/my-computer-boots-to-a-black-screen-what-options-do-i-have-to-fix-it

Тут установка драйвера 
https://askubuntu.com/questions/47506/how-do-i-install-additional-drivers

#### Check Nvidia GPU

- nvidia-smi
- watch -n 1 nvidia-smi

### First commands on new OS Ubuntu

- whoami
- sudo apt-get update
- sudo apt-get install aptitude
- sudo aptitude safe-upgrade

#### Table of processes

- top

%CPU — процент доступного времени процессора, которое использовала запущенная программа

%MEM — процент использования оперативной памяти данным процессом

#### Check virtual networks and IP

- ifconfig -a

### working with hardware on Ubuntu

- hwinfo --short

#### Processor utilization

Check [this](https://romka.eu/blog/metrika-zagruzhennosti-processora-cpu-utiliztion-eto-ne-chto-vy-dumaete) article

- sudo perf stat -a --sleep 10

![](https://github.com/IgorSondors/cheatsheet/blob/master/images/2.jpg)

![](https://github.com/IgorSondors/cheatsheet/blob/master/images/3.jpg)

#### Check RAM

- sudo lshw -C memory

### Ssh connection

- ssh root@ip

### Files transfer

#### Вводить на локальной машине 
#### для переноса с локальной на удаленную

- scp -r /home/sondors/Recognizer/cloud_server/neurohives root@138.68.65.54:~/cloud_server/neurohives

#### для переноса с удаленной на локальную

- scp root@164.90.220.22:/~/watahell.png  /home/sondors/Recognizer/server/not_api

### Markdown cheatsheet

- [link](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

### Errors that was problem for me

![](https://github.com/IgorSondors/cheatsheet/blob/master/images/failed_conv.jpg)

- Чекай [документацию](https://www.tensorflow.org/guide/gpu)

- TF дефолтно занимает всю память, это ее освобождает
```python

import tensorflow as tf
gpus = tf.config.experimental.list_physical_devices('GPU')
if gpus:
    # Restrict TensorFlow to only allocate 6GB of memory on the first GPU
    try:
        tf.config.experimental.set_virtual_device_configuration(
            gpus[0],
            [tf.config.experimental.VirtualDeviceConfiguration(memory_limit=6144)])
        logical_gpus = tf.config.experimental.list_logical_devices('GPU')
        print(len(gpus), "Physical GPUs,", len(logical_gpus), "Logical GPUs")
    except RuntimeError as e:
        # Virtual devices must be set before GPUs have been initialized
        print(e)
```
- Для проверки выполнения работы TF на GPU

```python
import os
os.environ["CUDA_VISIBLE_DEVICES"] = "0"
import tensorflow as tf
if tf.test.is_built_with_cuda() and tf.test.is_gpu_available(cuda_only=False, min_cuda_compute_capability=None):
    print('You can use GPU')

else:
    print('TF can not use GPU')
```
