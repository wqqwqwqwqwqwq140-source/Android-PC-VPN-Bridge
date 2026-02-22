EN
# Android-PC-VPN-Bridge
is a bundle of two applications that allows your computer to use a VPN connection running on an Android smartphone. 
PC traffic is redirected through a SOCKS5 proxy on the phone, which in turn goes through an active VPN (any - OpenVPN, WireGuard, built-in, etc.).

## Why is it needed?
- Bypassing blocks on a PC without the need to configure a VPN on the computer itself.
- Using an expensive/corporate VPN only on your phone, while your PC traffic goes through it.
- If your ISP blocks internet sharing (tethering), a proxy server on your phone often goes unnoticed.

## Project structure
1. **Android app** (`VpnProxy`) - runs a SOCKS5 proxy on your phone. Requires an active VPN.
2. **PC Client** (`PCClient.java`) is a Java program with a graphical interface for connecting to a proxy and automatically configuring browsers (with restrictions).

## PC Client Features
- Connecting to a SOCKS5 proxy on a phone using IP and port.
- Checking

RU
# Android-PC-VPN-Bridge
это связка из двух приложений, позволяющая вашему компьютеру использовать VPN-соединение, запущенное на Android-смартфоне.  
Трафик ПК перенаправляется через SOCKS5-прокси на телефоне, который, в свою очередь, идёт через активный VPN (любой — OpenVPN, WireGuard, встроенный и т.д.).

## Зачем это нужно?
- Обход блокировок на ПК без необходимости настраивать VPN на самом компьютере.
- Использование дорогого/корпоративного VPN только на телефоне, а трафик ПК проходит через него.
- Если ваш оператор блокирует раздачу интернета (режим модема) — прокси-сервер на телефоне часто остаётся незамеченным.

## Состав проекта
1. **Android-приложение** (`VpnProxy`) — запускает SOCKS5-прокси на телефоне. Требуется включённый VPN.
2. **ПК-клиент** (`PCClient.java`) — Java-программа с графическим интерфейсом для подключения к прокси и автоматической настройки браузеров (с ограничениями).

## Возможности ПК-клиента
- Подключение к SOCKS5-прокси на телефоне по IP и порту.
- Проверка через внешний API (httpbin.org/ip) — отображает ваш IP через VPN.
- Автоматическая настройка:
  - **Firefox** — через модификацию `prefs.js` (устанавливает SOCKS5 с DNS через прокси).
  - **Системный прокси Windows** (HTTP/HTTPS) — для Chrome, Edge и других браузеров, использующих системные настройки.
- Сохранение исходных настроек и их восстановление при отключении или выходе.
- Двуязычный интерфейс (русский/английский) с переключением на лету.
- Диалог подтверждения при закрытии с автоматическим сбросом настроек.

## Важные ограничения (почему автонастройка может работать "хуево")
- ⚠️ **Системный прокси Windows поддерживает только HTTP/HTTPS**, но не SOCKS5. Поэтому Chrome, Edge и Opera после включения системного прокси будут работать только с HTTP-сайтами, а HTTPS-трафик может не пойти через прокси. Для полноценной работы используйте Firefox или программы типа Proxifier.
- ⚠️ **Firefox** настраивается корректно (SOCKS5 + DNS через прокси), но изменения вступают в силу только после перезапуска браузера.
- ⚠️ Программа не может автоматически настроить все браузеры идеально из-за ограничений самих браузеров и ОС.

## Инструкция по использованию

### На телефоне
1. Установите Android-приложение `VpnProxy` (исходники в папке `android`).
2. Включите любой VPN на телефоне.
3. Запустите приложение, нажмите **«Запустить прокси»**. На экране появится IP-адрес телефона в локальной сети (например, `192.168.1.10`) и порт `1080`.

### На ПК
1. Убедитесь, что установлена Java Runtime (JRE) версии 8 или выше.
2. Скачайте `PCClient.jar` или скомпилируйте из исходников (`javac PCClient.java`, `jar cfe PCClient.jar PCClient *.class`).
3. Запустите: `java -jar PCClient.jar`.
4. Введите IP телефона и порт, нажмите **«Подключиться»**.
5. Выберите, какие браузеры настраивать (Firefox и/или системный прокси).
6. После успешной проверки IP вы увидите сообщение в логе.
7. Для Firefox потребуется перезапустить браузер.
8. При отключении или закрытии программы исходные настройки будут восстановлены.
