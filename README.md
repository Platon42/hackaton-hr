# Документация
Документация к ATS-системе [(Applicant Tracking System)](https://ru.wikipedia.org/wiki/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D0%BA%D0%B0%D0%BD%D0%B4%D0%B8%D0%B4%D0%B0%D1%82%D0%B0%D0%BC%D0%B8) `SmartHuman` - цифровому ассистенту для помощи HR-специалистам, разработанной на хакатоне «Цифровой Прорыв», финальный этап, заказчик решения - АО ГазПромБанк.

#### [**Ссылка на Прототип проекта**](http://130.193.46.118)

# Вступление и описание решения

Система `SmartHuman` является прототипом ATS-системы (Applicant Tracking System) для полноценной помощи HR-специалистам.

Она позволяет повысить скорость закрытия вакансий и качество работы с кандидатами. HR-специалист проводит весь цикл работы с цифровым ассистентом - принимает заявки на подбор специалиста, легко формирует текст вакансии, рассматривает рекомендуемые системой резюме кандидатов, отправляет приглашения на интервью и тестирование, дает соискателям обратную связь.

Система автоматически формирует текст вакансии с помощью технологий машинного обучения, проводит первичный скрининг резюме по множеству факторов, а также предлагает кандидатам альтернативные вакансии.

Уникальностью решения является не только удобный и понятный UX/UI-интерфейс, а также искусственный интеллект, который на всех этапах работы пользователя - обучается на его действиях и поступающих новых данных.

Стек проекта: `PHP`, `Symfony`, `PostgreSQL`, `Vue.JS`, `Python`, `Sklearn`, `Tensorflow`, `Docker`.

У нас есть [***рабочая MVP-версия (минимально работоспособная версия продукта)***](http://130.193.46.118), которая не только обладает удобным интерфейсом, но достаточным функционалом, чтобы продемонстрировать основные аспекты решения задачи кейса. Мы запустили ее на [внешнем сервере](http://130.193.46.118).

Спасибо организаторам за интересную задачу, мы будем рады продолжить сотрудничество!

# Техническое описание проекта
## Установка
Т.к. в проекте используется микросервисная архитектура, большая часть сервисов доступна для скачивания в виде контейнеров в [реджистри от GitHub](https://github.com/KusokBanana?tab=packages&repo_name=hackaton-hr).
Для локального развертывания решения необходимо авторизоваться в GitHub Package Registry [по инструкции](https://docs.github.com/en/free-pro-team@latest/packages/using-github-packages-with-your-projects-ecosystem/configuring-docker-for-use-with-github-packages#authenticating-to-github-packages) и в корне проекта выполнить команду `docker-compose up --build`

Важно, что у вас должен быть установлен и запущен `Docker`.

> После того, как установка всех необходимых зависимостей будет выполнена, вы сможете потестировать систему локально по ссылке http://localhost/

## Структура
Проект представляет собой монорепозиторий. Ниже структура директорий:
```
.
├── Makefile
├── README.md
├── api - backend проекта (Symfony)
├── docker-compose.yaml
├── frontend - frontend проекта (Vue.js)
│   ├── Dockerfile
│   ├── Makefile
│   ├── README.md
│   ├── babel.config.js
│   ├── nginx
│   ├── package-lock.json
│   ├── package.json
│   ├── postcss.config.js
│   ├── public
│   ├── src
│   ├── tailwind.config.js
│   └── vue.config.js
├── docker - докерфайлы
│   ├── frontend
│   ├── nginx
│   ├── php-fpm
└── prediction - модели ML
    ├── RUGPT3.ipynb - ruGPT-3, прототип конструктора вакансий
    ├── resume_sample.ipynb
    ├── resume_to_vacancy.ipynb - метчинг резюме и вакансии
```
Исходный код серверной части — в папке `api`, исходный код браузерной части приложения — в папке `frontend`. Кроме того, данные по разработке модели в директории `prediction`, а данные по инфраструктурным вопросам в `dockerfile`

Каждая директория по возможности содержит файл `Makefile` с базовыми командами.

## Архитектура приложения
Приложение состоит из микро-сервисов, включая сервис авторизации, сервис моделей, сервис-ui и  т.д. 
ML модели размещены отдельно и запускаются в docker-контейнерах в требуемом окружении.

# Дополнительные материалы

- [**Прототип проекта, т.е. рабочая MVP-версия (минимально работоспособная версия продукта)**](http://130.193.46.118).
- [Предварительная дорожная карта и смета](https://docs.google.com/spreadsheets/d/1zUvYpD-8AqFN9PVyzifXM-AuFRmsubhW-nvbBfRgReA/edit?usp=sharing) общих затрат по разработке и внедрению на архитектуре банка - как минимальной, так и дополнительно масштабируемой версии проекта.
