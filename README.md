# Домашнее задание к занятию "Система мониторинга Zabbix 2" - Марчук Кирилл



### Задание 1 Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.


1. `В веб-интерфейсе Zabbix Servera в разделе Templates создаём новый шаблон`
2. `Создаём Item который будет собирать информацию об загрузке CPU`
3. `Создаём Item который будет собирать информацию об загрузке RAM`


```

```


![Задание 1](https://github.com/ottofonciceron-coder/GitLab-8-03-hw/blob/main/Задание%201.png)`

---

### Задание 2 Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>..



1. `Установил Zabbix Agent на 2 вирт.машины`
2. `Добавил Zabbix Server в список разрешенных серверов своих Zabbix Agentов`
3. `Добавил Zabbix Agentов в раздел Configuration > Hosts своего Zabbix Servera`
4. `Добавил Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera`
5. `В разделе Latest Data начали появляться данные с добавленных агентов`
6. 

```
wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb
sudo apt update
sudo apt install zabbix-agent -y
sudo nano /etc/zabbix/zabbix_agentd.conf  # редактирование Server, ServerActive, Hostname
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
sudo systemctl status zabbix-agent

```

---

### Задание 3 Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.



1. `В настройках каждого хоста и в разделе Templates прикрепляем к этому хосту наш шаблон`
2. `Так же к каждому хосту привязываем шаблон Linux by Zabbix Agent`
3. `Проверяем что в раздел Latest Data начали поступать необходимые данные из нашего шаблона`


```

```


![Задание 2-3](https://github.com/ottofonciceron-coder/GitLab-8-03-hw/blob/main/Задание%202-3.png)`


---

### Задание 4 Создайте свой кастомный дашборд.


1. `В разделе Dashboards создаём новый дашборд`
2. `Размещаем на нём несколько графиков на своё усмотрение.`


```

```


![Задание 4](https://github.com/ottofonciceron-coder/GitLab-8-03-hw/blob/main/Задание%204.png)`

---
