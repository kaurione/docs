# Technical description in English

- [General info](#general-info)
  - [API calls](#api-calls) 
  - [Currencies](#currencies)
  - [Exchange services](#exchange-services)
  - [Payment gateways](#payment-gateways)
  - [Verification providers](#verification-providers)
- [Functionality description per module](#functionality-description-per-module)
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
- [Infrastructure](#infrastructure)
  - [General info](#general)
  - [Docker containers overview](#docker-containers-overview)
  - [Deployment scheme](#deployment-scheme)
- [First deploy](#first-deploy)
  
  
 
## General info

Programming language - Python 3.5

Packages used:

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


Modules of the project:

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

 
### API calls

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

### Currencies

Currencies available in the distribution package - BTC, ETH, USDT(ERC 20), UAH, RUB, USD,EUR
 
### Exchange services

Kraken, Binance, Huobi

### Payment gateways

1. Crypto Node Provider for BTC
2. Crypto Node Provider for ETH
3. Crypto Node Provider for USDT(ERC20)
4. Cypix for RUB
5. FOUR_BILL, XPAY, Billine, GlobalPay, Paysoft, Colibri for UAH  

### Verification providers

1. SumSub
2. Provider requested by the client

## Functionality description per module


#### kauri_rest_api_account

This module includes:

1. Account creation logic
2. Differentiation of accounts into types, accounts disabling and verification by the system operator
3. Generation of API key and secret key for authorization
4. JWT token authorization, Telegram bot authorization, API keys authorization
5. Password reset
6. The logic of adding IP to whitelist by account
7. Using a provider for automatic verification


#### kauri_rest_api_balance

 This module includes:

1. Maintaining user balances
2. Maintaining balances of payment gateways / exchange services
3. Total amount of payment obligations towards users
4. Total amount of funds in the system
5. An option to set up notifications for when the balance in a payment system or exchange service is less than expected


#### kauri_rest_api_callbacks

This module is an API endpoint with the main task of receiving notifications from payment systems and transfer information to the system


#### kauri_rest_api_core

This module configures currencies, currency pairs, providers, with the option to enable/disable them


#### kauri_rest_api_deposit_order

This module is responsible for processing deposit payments.

It includes:

1. Information on deposits
2. Information on the created deposit addresses
3. Enabling/disabling of deposit address generation
4. Settings for commissions and limits for users
5. Settings for specifying the cost of the deposit for the provider (for calculating the profit)
6. Settings for auto-conversion of funds on per-user basis
7. Connected transaction analysis


#### kauri_rest_api_exchange_order

The module is responsible for processing exchange operations, it includes the following features:

1. Enabling / disabling the exchange for a currency pair, for all currency pairs, for user groups or for a specific user
2. Setting exchange limits
3. Setting up an exchange for a pair (with a buyback on the exchange service or without)
4. Logging of the buyback operation
5. Buyback settings
6. Separate buyback logic described in this document


#### kauri_rest_api_exchange_provider

The module is responsible for integration with exchange services and performing operations. Downloads trades and displays them for orders that were placed by the system


#### kauri_rest_api_exchange_rate

The module is responsible for pricing policy, it is possible to set a static price for the selected pair, specify a price formation expression for the selected pair, there is a separate logic for the accumulation of historical data on prices that are broadcast by the system


#### kauri_rest_api_internal_movement_order

The module is responsible for the internal transfers of funds between users. It is possible to specify limits, fees, disable or enable the operation for user groups or for a specific user.

#### kauri_rest_api_notification

The module is responsible for sending email, Telegram messages. It is possible to customize email templates, Telegram message templates by the operator via admin panel. It is possible to create a mailing list including all users in the system.

The distribution package includes the ability to send messages via Slack, Telegram.

There are two email providers.

#### kauri_rest_api_order_core

This module stores general information on all orders, where to send the callback if it was specified during creation, the history of sent callbacks.


#### kauri_rest_api_payment_provider

The module is made similarly to "exchange provider", its main task is to communicate with gateways via API


#### kauri_rest_api_report
This module generates scheduled and on demand reports

#### kauri_rest_api_wallet

This module is responsible for generating wallets (payment links)


#### kauri_rest_api_withdrawal_order

This module is responsible for processing withdrawal orders. 

It includes:

1. Withdrawal enable / disable settings
2. Settings for limits and fees for the operation
3. Option to specify the priority of providers for withdrawal
4. Configurations for providers (waiting time between transactions, minimal and maximal transaction etc.) 
5. Option to manually close the withdrawal order if the payment gateway has not responded with the final status for the transaction or transactions
6. Option to send withdrawals for additional check by the operator
7. Ability to confirm withdrawals via email (TOTP code)

#### kauri_rest_api_invoice_order

This module is responsible for issuing invoices and processing payments on them. The module includes the basic settings - enable / disable, fees and limits settings (limits are specified in usd). Also settings for the invoice itself (lifetime, etc.). There is an option to specify fees on conversion if the user pays in another currency


#### kauri_rest_api_fast_exchange_order

This module is responsible for the currency exchange, giving user the ability to pay in one currency and receive another currency.

It is possible to customize the exchange rate.

As with all orders, there are settings for enable / disable, limits, fees.


## Infrastructure


### General

The project consists of a web application, RabbitMQ broker and workers, database, and Redis.

Initially, nginx accepts the API request, sends it to UWSGI, which processes this request. The project provides for configuring of UWSGI server. Out of the box, you can configure UWSGI to raise the number of processes that are needed at a given time and reach a certain maximum value.

There is a separate UWSGI process that only listens to callbacks from payment services.

Each module is a docker container that has its own deploy file. When the container starts, a .py file that adds the necessary default values (currencies etc.) is run. If necessary, a queue or queues are created within one container. Initially, supervisor makes sure that the process for the listeners is raised and there you can safely configure the number of processes needed for a particular queue. Each module has its own .sh file that is run as a part of the startup of the docker container and as a result it is a running process or processes by UWSGI or Celery.

Docker containers are configured via docker-compose files with a differentiation into environments


### Docker containers overview

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

The above is the list of containers that are deployed to both prod and test environments in a specific sequence.

db (DEV)  
rabbit (DEV and PROD)  
redis (DEV only)

Depending on the environment specified - the system will start the necessary docker containers


###  Deployment scheme

There are two versions of the environment - DEV, PROD. The only difference is that for DEV environment, the database and Redis is raised via docker, and for PROD this item is skipped. Depending on which environment was selected, at startup the system selects one or another “settings.py” file, which contains all the settings (connection strings, etc.)

Deployment scheme:

1. Building a new docker image (new dependencies, the folder with the code is mounted)
2. Checks whether it is needed to create containers for rabbit, redis, db. 
3. Re-creation of the "web" container, the start of which means that all migrations passed, the start of API endpoint and API callbacks endpoint
4. If "web" container starts successfully, the command is executed to build other containers - this is where the workers are located


## First deploy

1\) Docker version not lower than (Docker version 18.09.6, build 481bc77) and docker-compose version not lower than (docker-compose version 1.22.0, build f46880fe) must be installed on the new environment.

2\) Repository from git should be downloaded

3\) Regardless of the environment (DEV or PROD), you need to specify the "correct" settings.py file and write the necessary settings for it or override the settings.
All settings are in the file rest_api/kauri_rest_api/kauri_rest_api/settings/base.py 

Local settings file:
rest_api/kauri_rest_api/kauri_rest_api/settings/local.py  
 
Using it as an example, you can look up what needs to be redefined.
If you need to use other "settings.py" instead of "local", you need to write out an environment variable in the .env file, which points at the settings file intended for use.

4\) Run "sh run_deployment.sh \<DEV or PROD>" and the deployment will start. If there are errors, they will be shown at the start of containers
