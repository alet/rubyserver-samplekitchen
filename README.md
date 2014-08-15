# Настройка сервера

Example of use [rubyserver](https://github.com/alet/rubyserver) cookbook 

## На рабочей станции 

* должен быть настроен вход по ключу на сервер
* должены быть установлены
```bash
gem install knife-solo berkshelf --no-ri --no-rdoc
```
либо зайти в папку с кухней и выполнить
```bash
bundle install
```

## Настройка

* относительный путь к конфигурации сервера - nodes/node.json
* версию руби нужно указывать полностью, до патча (1.9.3-p547)
* базу нужно указывать того типа, которую нужно установить (PostgreSQL | MySQL). В случае PostgreSQL база не создаётся из-за бага [issue](http://tickets.opscode.com/browse/COOK-1406), но указывать нужно для установки нужной базы данных. Если указать оба вида базы данных, будут установлены оба.
* доменное имя для почты берётся из FQDN, поэтому у сервера должно быть указано имя (команда hostname --fqdn должна выводить имя сервера)
* DKIM запись для домена можно найти в файле /etc/mail/mail.txt на сервере

## Собственно установка сервера (команды выполняются на рабочей станции)

* зайти в папку со скриптами конфигурации
* для сервера на Ubuntu нужно установить переменную LC_ALL
```bash
export LC_ALL=en_US.UTF-8
```
* собственно установка:
```bash
knife solo bootstrap USER@SERVER nodes/node.json -P PASSWORD --bootstrap-version 11
```
* очистка:
```bash
knife solo clean USER@SERVER -P PASSWORD
```
