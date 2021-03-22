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
### Docker install and commands

#### Installation

```shell

curl -fsSL get.docker.com -o get-docker.sh

```
```shell

sh get-docker.sh

```
- install docker-machine

```bash

base=https://github.com/docker/machine/releases/download/v0.16.0 &&
  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
  sudo mv /tmp/docker-machine /usr/local/bin/docker-machine &&
  chmod +x /usr/local/bin/docker-machine
 
  ```
  - install docker-compose
  ```bash
  
  sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```

```bash

sudo chmod +x /usr/local/bin/docker-compose

```

#### Docker image create and push

```bash
sudo docker container run -it -p 8080:8080 ubuntu:18.04
```

```bash
sudo docker container commit amazing_montalcini
```

```bash
sudo docker image tag a7fd027daf79 igorsondors/cloud_server
```

```bash
sudo docker image push igorsondors/cloud_server
```
- for creation of image with Dockerfile

```bash
sudo docker build . --tag pyramid
```

#### Git working

```
git clone https://github.com/IgorSondors/123.git
```
```
cd 123
```
```
git init
```
```
git add README.md
```
```
git commit -m "first commit"
```
```
git branch -M main
```
Команда ниже не нужна при git clone
```
git remote add origin https://github.com/IgorSondors/123.git
```
```
git push -u origin main
```

#### Docstring styles

- [link](https://stackoverflow.com/questions/3898572/what-is-the-standard-python-docstring-format/24385103#24385103)

#### OCR Synth generators

- [Max Jaderberg's word-level renderer](https://bitbucket.org/jaderberg/text-renderer/src/master/) - генератор полос, на который ссылался Ankush
- [trdg](https://github.com/Belval/TextRecognitionDataGenerator/tree/master/trdg) - генератор полос с различными модами включающими в себя кастомные бэкграунды, шумы повороты, рукописный текст
- [SynthText](https://github.com/ankush-me/SynthText) - OCR in the wild генератор, текст имеет структуры бэкграунда, но иногда рендерится слабо видимым
- [Sanster](https://github.com/Sanster/text_renderer) - генератор полос с поддержкой GPU вычислений

#### OCR Datasets

- [ICDAR](https://rrc.cvc.uab.es/?ch=15) - реальный датасет для локализации следующих языков Chinese, Japanese, Korean, English, French, Arabic, Italian, German and Indian

- [TotalText](https://github.com/cs-chan/Total-Text-Dataset) - 1500 реальных картинок изогнутого eng текста с разметкой полигонами и метками 

- [The Street View Text Dataset](http://vision.ucsd.edu/~kai/svt/) - real data

- [MJSynth](https://www.robots.ox.ac.uk/~vgg/data/text/) - 10Gb eng синтетические полосы Jaderberg

- [SynthText in the Wild dataset (41G)](https://www.robots.ox.ac.uk/~vgg/data/scenetext/) - dataset consists of 800 thousand images with approximately 8 million synthetic word instances. Each text instance is annotated with its text-string, word-level and character-level bounding-boxes.

