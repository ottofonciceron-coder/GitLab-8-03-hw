# Домашнее задание к занятию 1 "Disaster recovery и Keepalived" - Марчук Кирилл



### Задание 1 На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.



1. `Настраиваем отслеживание состояния интрефейсов`
2. `Делаем имитацию разрыва соединения и проверям через Ping`



```
маршрутизатор 1
enable
configure terminal
interface GigabitEthernet0/0
standby 1 ip 192.168.10.1
standby 1 priority 110
standby 1 preempt
standby 1 track GigabitEthernet0/0 20
exit

маршрутизатор 2
enable
configure terminal
interface GigabitEthernet0/0
standby 1 ip 192.168.10.1
standby 1 priority 100
standby 1 preempt
standby 1 track GigabitEthernet0/0 20
exit

```


![Router 1](https://github.com/ottofonciceron-coder/Disaster-recovery-Keepalived-git-hw/blob/main/Router1.png)`

![Router 2](https://github.com/ottofonciceron-coder/Disaster-recovery-Keepalived-git-hw/blob/main/Router%202.png)`

![Router 2](https://github.com/ottofonciceron-coder/Disaster-recovery-Keepalived-git-hw/blob/main/Router%2022.png)`

---

### Задание 2 Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived и Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html



1. `Установил 2 вирт.машины и устанавливаем и настраиваем сервис Keepalived`
2. `Настраиваем веб-сервер nginx на 2 вирт.машинах`
3. `Написали Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html`
4. `Настраиваем Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер (BACKUP)`


```
# СКРИПТ

#!/bin/bash

WEB_PORT=80
WEB_ROOT="/var/www/html"
INDEX_FILE="$WEB_ROOT/index.html"

# Проверяю, слушает ли порт
nc -z localhost $WEB_PORT
if [ $? -ne 0 ]; then
  echo "Port $WEB_PORT is down"
  exit 1
fi

# Проверяю наличие index.html
if [ ! -f "$INDEX_FILE" ]; then
  echo "File $INDEX_FILE missing"
  exit 1
fi

# Если Всё Хорошо
exit 0

#КОНФИГ keepalived.conf MASTER

vrrp_script chk_web {
    script "/etc/keepalived/check_web.sh"
    interval 3
    fall 2
    rise 2
}

vrrp_instance VI_1 {
    state MASTER
    interface eth0
    virtual_router_id 51
    priority 100
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1234
    }

    virtual_ipaddress {
        192.168.10.100
    }

    track_script {
        chk_web
    }
}

#КОНФИГ keepalived.conf BACKUP

vrrp_script chk_web {
    script "/etc/keepalived/check_web.sh"
    interval 3
    fall 2
    rise 2
}

vrrp_instance VI_1 {
    state BACKUP
    interface eth0
    virtual_router_id 51
    priority 90
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1234
    }

    virtual_ipaddress {
        192.168.10.100
    }

    track_script {
        chk_web
    }
}


```

![MASTER](https://github.com/ottofonciceron-coder/Disaster-recovery-Keepalived-git-hw/blob/main/Master%20тест%20.png)`

![BACKUP](https://github.com/ottofonciceron-coder/Disaster-recovery-Keepalived-git-hw/blob/main/BACKUP.png)`


---
