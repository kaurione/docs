# Техническое описание проекта

- [Общая информация](#общая-информация)
  - [Список API вызовов, которые входят в сборку](#список-api-вызовов-которые-входят-в-сборку) 
  - [Список валют](#список-валют)
  - [Список биржевых провайдеров](#список-биржевых-провайдеров)
  - [Список платежных шлюзов](#список-платежных-шлюзов)
  - [Список провайдеров на верификацию](#список-провайдеров-на-верификацию)
- [Описание функционала по модулям](#описание-функционала-по-модулям)
  - [kauri_rest_api_account](#kauri_rest_api_account)
  - [kauri_rest_api_balance](#kauri_rest_api_balance)
  - [kauri_rest_api_callbacks](#kauri_rest_api_callbacks)
  - [kauri_rest_api_core](#kauri_rest_api_core)
  - [kauri_rest_api_deposit_order](#kauri_rest_api_deposit_order)
  - [kauri_rest_api_exchange_order](#kauri_rest_api_exchange_order)
  - [kauri_rest_api_exchange_provider](#kauri_rest_api_exchange_provider)
  - [kauri_rest_api_exchange_rate](#kauri_rest_api_exchange_rate)
  - [kauri_rest_api_internal_movement_order](#kauri_rest_api_internal_movement_order)
  - [kauri_rest_api_notification](#kauri_rest_api_notification)
  - [kauri_rest_api_order_core](#kauri_rest_api_order_core)
  - [kauri_rest_api_payment_provider](#kauri_rest_api_payment_provider)
  - [kauri_rest_api_report](#kauri_rest_api_report)
  - [kauri_rest_api_wallet](#kauri_rest_api_wallet)
  - [kauri_rest_api_withdrawal_order](#kauri_rest_api_withdrawal_order)
  - [kauri_rest_api_invoice_order](#kauri_rest_api_invoice_order)
  - [kauri_rest_api_fast_exchange_order](#kauri_rest_api_fast_exchange_order)
- [Инфраструктура](#инфраструктура)
  - [Общие детали](#общие-детали)
  - [Обзор докер контейнеров](#обзор-докер-контейнеров)
  - [Схема деплоймента](#схема-деплоймента)
- [Первый деплой системы](#первый-деплой-системы)
  
  
 
## Общая информация

Язык программирования - Python 3.5

Библиотеки, которые используются:

1. anyjson==0.3.3
2. billiard==3.3.0.23
3. celery==3.1.20
4. Django==2.0.2
5. kombu==3.0.37
6. djangorestframework==3.7.7
7. uWSGI==2.0.17
8. django-rest-swagger==2.1.2
9. coreapi==2.3.3
10. django-extensions==2.0.7
11. beautifulsoup4==4.6.0
12. djangorestframework-jwt==1.11.0
13. mysqlclient==1.3.13
14. zeep==3.2.0
15. graypy==0.3.2
16. Sqlalchemy==1.2.17
17. gevent==1.2.2
18. requests[socks]==2.23.0
19. django_redis==4.12.1
20. django_otp==0.5.2
21. qrcode==6.1
22. mandrill==1.0.57
23. sympy==1.4
24. PyCryptodome==3.8.2
25. django-admin-rangefilter==0.5.0
26. xmltodict==0.12.0
27. python-telegram-bot==12.0.0
28. qrcode==6.1
29. luhn==0.2.0
30. django-ajax-selects==1.8.0
31. oauth2client==4.1.3
32. gspread==3.2.0
33. qrcode[pil]==6.1
34. admin-totals==1.0.1
35. slackclient==1.3.2
36. html-slacker==0.1.6


Модули, которые входят в состав проекта:

1. kauri_rest_api
2. kauri_rest_api_core
3. kauri_rest_api_exchange_rate
4. kauri_rest_api_account
5. kauri_rest_api_wallet
6. kauri_rest_api_balance
7. kauri_rest_api_order_core
8. kauri_rest_api_deposit_order
9. kauri_rest_api_withdrawal_order
10. kauri_rest_api_exchange_order
11. kauri_rest_api_exchange_provider
12. kauri_rest_api_payment_provider
13. kauri_rest_api_notification
14. kauri_rest_api_report
15. kauri_rest_api_callbacks
16. kauri_rest_api_internal_movement_order
17. kauri_rest_api_invoice_order
18. kauri_rest_api_fast_exchange_order
19. kauri_rest_api_payment_card

 
### Список API вызовов, которые входят в сборку

1. api/v1/currency
2. api/v1/pair
3. api/v1/exchange_rate/history
4. api/v1/exchange_rate
5. /api/v1/user/account/setting
6. /api/v1/user/account_info
7. /api/v1/user/api_keys/create
8. /api/v1/user/api_keys/delete
9. /api/v1/user/api_keys/verify
10. /api/v1/user/balance
11. /api/v1/user/change_password
12. /api/v1/user/create
13. /api/v1/user/create_from_telegram
14. /api/v1/user/disable_2fa
15. /api/v1/user/email/verify
16. /api/v1/user/enable_2fa
17. /api/v1/user/obtain_token
18. api/v1/user/refresh_token
19. api/v1/user/reset_password/send_link
20. api/v1/user/reset_password/set_new_password
21. api/v1/user/telegram/assign
22. api/v1/user/telegram/unassign
23. api/v1/user/telegram/verify
24. api/v1/user/totp/qr_code
25. api/v1/user/totp/verify
26. api/v1/user/verification/start
27. api/v1/user/white_ip/create
28. api/v1/user/white_ip/delete
29. api/v1/orders/history
30. api/v1/orders/details
31. api/v1/user/account_info
32. api/v1/user/reset_password/send_link
33. api/v1/user/reset_password/set_new_password
34. api/v1/withdrawal/repeat
35. api/v1/withdrawal/cancel
36. api/v1/withdrawal
37. api/v1/exchange/calculate
38. api/v1/exchange/cancel
39. api/v1/exchange/repeat
40. api/v1/exchange
41. api/v1/internal_movement/repeat
42. api/v1/internal_movement
43. api/v1/statistics
44. api/v1/invoice/
45. /api/v1/invoice/details
46. /api/v1/invoice/pay
47. /api/v1/invoice/pay/public
48. /api/v1/fast_exchange
49. /api/v1/fast_exchange/calculate
50. /api/v1/fast_exchange/exchange_rate
51. /api/v1/fast_exchange/limits
52. /api/v1/deposit/
53. /api/v1/deposit/address
54. /api/v1/deposit/address/details
55. /api/v1/deposit/cancel
56. /api/v1/deposit/repeat

### Список валют

В дистрибутиве должны быть доступны валюты - BTC, ETH, USDT(ERC 20), UAH, RUB, USD,EUR
 
### Список биржевых провайдеров

Kraken, Binance, Huobi

### Список платежных шлюзов

1. Crypto Node Provider for BTC
2. Crypto Node Provider for ETH
3. Crypto Node Provider for USDT(ERC20)
4. Cypix для RUB
5. FOUR_BILL, XPAY, Billine, GlobalPay, Paysoft, Colibri для UAH  

### Список провайдеров на верификацию

1. SumSub
2. Провайдер по желанию клиента

## Описание функционала по модулям</span>


#### kauri_rest_api_account

В этот модуль входит:

1. Логика создания аккаунта
2. Разделение аккаунтов на типы, и виды, возможность их отключения, верификации оператором системы
3. Генерация апи ключа и секретного ключа, по которому возможна авторизация
4. Авторизация по JWT токену, авторизация для телеграм бота, авторизация через ключи
5. Восстановление пароля
6. Логика добавления IP в белый список по аккаунту
7. Использование провайдера на автоматическую верификацию


#### kauri_rest_api_balance

  В этот модуль входит:

1. Ведение балансов пользователей
2. Ведение балансов платежных шлюзов/бирж
3. Суммарное количество обязательств по пользователям
4. Суммарное количество средств в самой системе
5. Возможность настройки уведомления, если баланс на платежке или на бирже стал меньше ожидаемого


#### kauri_rest_api_callbacks

Модуль, который представляет собой API endpoint, основная задача которого принимать нотификации от платежных систем и передавать информацию дальше в систему


#### kauri_rest_api_core

В этом модуле настраиваются валюты, валютные пары, провайдеры, есть возможность отключение или включения


#### kauri_rest_api_deposit_order

Этот модуль отвечает за обработку депозитных платежей.

В него входит:

1. Информация по самим депозитам
2. Информация по созданным депозитным адресам
3. Настройки по включению/выключению получение адреса на пополнение
4. Настройки по комиссиям, лимитам для пользователей
5. Настройки по указанию стоимости депозита со стороны провайдера(для подсчёта профита)
6. Настройки по автоконвертации средств для конкретного пользователя
7. Подключенный анализ транзакций


#### kauri_rest_api_exchange_order

Модуль отвечает за обработку обменных операций,в него входят след.возможности:

1. Включение/выключение обмена по валютной паре, по всем валютным парам, для группы пользователей или для конкретного пользователя
2. Установка лимитов по обмену
3. Настройка обмена по паре(с откупом на бирже или нет)
4. Логирование операции откупа
5. Настройка откупа
6. Отдельная логика откупа, которая описана в этом документе

#### kauri_rest_api_exchange_provider

Модуль, отвечает за интеграцию с биржами и выполнению операций. Скачивает трейды и отображает по тем ордерам, которые выставлялись системой


#### kauri_rest_api_exchange_rate

Модуль отвечает за формирование цен, есть возможность настроить статическую цену по выбранной паре, указать для выбранной пары формулу формирование цены, есть отдельная логика по накоплению исторических данных по ценам, которые транслирует система

#### kauri_rest_api_internal_movement_order

Модуль, отвечает за внутренний перевод средств между пользователями. Есть возможность указать лимиты, фии, отключить или включить операцию для групп пользователей или для конкретного пользователя

#### kauri_rest_api_notification
Модуль отвечает за отправку писем, телеграмм сообщений. Есть возможность настройки шаблонов писем, шаблонов телеграмм сообщений через админку оператором. Есть возможность создания рассылки всем пользователям системы.

В поставку входит возможность отсылки сообщений через Slack, Telegram.
Есть два емейл провайдера

#### kauri_rest_api_order_core
В этом модуле хранится общая информация по всем заявкам, куда отправлять callback, если он был указан при создании, истории отправки коллбеков


#### kauri_rest_api_payment_provider
Модуль сделан по аналогии с “exchange provider”, его основная задача коммуницировать со шлюзами через API


#### kauri_rest_api_report
Данный модуль создает отчёт по расписанию и по требованию

#### kauri_rest_api_wallet
Данный модуль отвечает за генерацию кошельков(платежных ссылок)

#### kauri_rest_api_withdrawal_order
Модуль ответственный за обработка заявок на вывод, включает в себя:

1. Настройки по включению/выключению вывода
2. Настройки по указанию лимитов за операцию, фии
3. Возможность указывать приоритетность провайдеров на вывод
4. Возможность настройки провайдеров(время ожидания между транзакциями, минимальная, максимальная транзакция и т.д)
5. Возможность ручного закрытия заявки на вывод, если платежный шлюз не отдал финальный статус по транзакции или транзакциям
6. Возможность отправлять выводы на доп проверку оператором
7. Возможность подтверждать выводы через емейл(двухфакторным кодом)

#### kauri_rest_api_invoice_order

Этот модуль ответственный за то, что была возможность у пользователей выставлять счёт, обрабатывать платежи по нему. В состав модуля входят базовые настройки по модулю - включение/выключение, настройка комиссии, настройка лимитов(лимиты указываются в usd).Также есть настройки по самому счёту(время жизни, и т.д.). Для счёта есть возможность указывать фии по конвертации, если пользователь оплачивает другой валютой

#### kauri_rest_api_fast_exchange_order

Этот модуль ответственный за то, что была возможность у пользователя поменять одну валюту на другую, имея возможность оплатить одной валютой и получить другую валюту.

Есть возможность кастомизировать курс по которому будет происходить обмен.

Как и у всех заявок есть лимиты, фии, возможность отключения


## Инфраструктура


### Общие детали

Проект состоит из web-приложения, rabbitmq брокера и воркеров, базы данных, redis.
Изначально nginx принимает АПИ запрос, потом он его передает на UWSGI, который запрос и обрабатывает. В проекте предусмотрена конфигурирование настроек UWSGI сервера. Из коробки можно настроить, чтобы UWSGI поднимал количество процессов которые нужны на данный момент времени и доходил до какого-то максимального значения.

Предусмотрен отдельный uwsgi процесс, который слушает только “коллбеки” от платежных сервисов.

Каждый модуль представляет из себя - докер контейнер, у которого есть свой деплой файлик, при старте контейнера запускается .py файл, который добавляет нужные дефолтные значения(валюты и т.д.) Если нужно создается очередь или очереди в рамках одного контейнера. Изначально супервизор следит за тем, чтобы процесс для слушателей был поднят и там можно спокойно конфигурировать количество процессов нужные для той или иной очереди.У каждого модуля есть свой .sh файлик, который запускается в рамках старта докер контейнера и как результат это запущенный процесс или процессы от uwsgi или от celery.

Настройка докер контейнеров сделана через docker-compose файлы с разбиением на окружение


### Обзор докер контейнеров

web  
celery_beat  
internal_movement_order_operations   
report_operations  
notification_operations  
balance_operations  
account_operations  
exchange_order_operations  
withdrawal_order_operations  
wallet_operations  
deposit_order_operations  
exchange_provider_operations  
payment_provider_gateway_operations  
invoice_order_operations  
fast_exchange_order_operations

Приведенный список, это список контейнеров, которые деплоятся и на prod, и на тестовом окружении в определенной последовательности.

db (DEV)  
rabbit (DEV и PROD)  
redis (только DEV)

В зависимости от указанного окружения - система сама запустит нужные докер контейнера


###  Схема деплоймента

Есть две версии окружения - DEV, PROD. Разница состоит только в том, для DEV окружения база данных, redis поднимается из под докера, а для PROD - этот пункт пропускается. В зависимости какое окружение было выбрано, при старте система выбирает тот или иной “settings.py”, в котором прописаны все настройки(connection strings и т.д)

Схема деплоя:

1. Построение новое докер-образа(новые зависимости, монтируется папка с кодом)
2. Проверка нужно ли создавать rabbit, redis, db - контейнера
3. Запуск пересоздание контейнера “web”, запуск которого означает прохождение всех миграций, старт API ендпоинта и API callbacks ендпоинта
4. При успешном старте “web” контейнера выполняется команда на построение других контейнеров - это там где находятся воркеры


## Первый деплой системы

1\) На новом окружении должны быть установлены docker версией не ниже чем (Docker version 18.09.6, build 481bc77) и docker-compose, версией не ниже чем (docker-compose version 1.22.0, build f46880fe).

2\) Нужно скачать репозиторий из git

3\) Вне зависимости от окружения (DEV или PROD) нужно указать “правильный” settings.py файл и прописать нужные для него настройки или сделать переопределение настроек.  
Все настройки находятся в файле rest_api/kauri_rest_api/kauri_rest_api/settings/base.py  

Файл с локальными настройками:  
rest_api/kauri_rest_api/kauri_rest_api/settings/local.py  
 
На его примере можно глянуть, что нужно переопределять.  
Если нужно использовать другой “settings.py”, не “local”, нужно в .env файле прописать переменную окружения, которая ведёт к settings файл, который нужно использовать.

4\) Запустить “sh run_deployment.sh \<DEV or PROD>”, и запустится процесс деплоймента. Если будут ошибки, по старту контейнеров, они будут показаны

