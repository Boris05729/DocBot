---
  Техническое задание на разработку Телеграм
  бота для регистрации и хранения документов
---

# Общее описание проекта

Проект заключается в разработке набора скриптов для взаимодействия с
Телеграм ботом, который предназначен для регистрации и хранения
входящих, исходящих и внутренних документов. Бот предоставляет
возможность автоматизированной обработки документов с помощью интервью с
пользователями и регистрации документов в соответствующих журналах.

**Основные характеристики:**

**Операционная система:** Debian  
**Язык программирования:** BASH  
**Назначение:** Телеграм бот для регистрации и хранения документов  
**Серверная часть:** Легкий дистрибутив Debian, разворачиваемый на
облачной виртуальной машине с предустановленными зависимостями и
скриптами  
**Бэкенд:** Набор BASH скриптов, каждый скрипт выполняет одну функцию  
**Журнал регистрации документов:** HTML страницы для журналов
входящих, исходящих и внутренних документов

# Бекенд (серверная часть)

Серверная часть разработана на базе облегченного дистрибутива Debian,
который разворачивается на облачной виртуальной машине. Предустановлены
все необходимые зависимости для работы с Телеграм ботом. Бот реализован
на языке BASH, а взаимодействие с **Телеграм API** осуществляется через
отдельные скрипты. Каждая функция бота реализована отдельным скриптом,
каждый из которых подробно описан ниже.

## Перечень функций (скриптов)

+ **/help -- Справка**

**Описание:** Команда выводит справку с детальной информацией по
    работе с ботом. Для каждой группы пользователей предусмотрена своя
    версия справки, текст которой хранится в файле manual_USERNAME.
  
**Использование:** Пользователь отправляет команду /help, бот
    проверяет группу пользователя и возвращает соответствующую справку.

+ **/get_No** -- Получить исходящий номер
  
**Описание:** Команда выдает следующий свободный номер для исходящих
    документов, который может быть использован для регистрации
    документов.
  
**Использование:** Пользователь отправляет команду /get_No, бот
    выдает номер, который сохраняется в журнале исходящих документов.
  
+ **Событие: отправка документа (pdf или JPEG)**
  
**Описание:** При отправке файла бот инициирует интервью с
    пользователем для сбора информации о документе. Вопросы и ответы для
    интервью берутся из файла конфигурации structure.conf.
  
**Использование:** Пользователь отправляет файл, бот задает вопросы
    о типе документа, проекте и комментарии, после чего документ
    сохраняется в соответствующем каталоге.
  
+ **Обработка входящих документов**
  
**Описание:** Бот автоматически присваивает порядковый номер
    входящему документу, сохраняет его и регистрирует в журнале входящих
    документов.
  
**Использование:** Документ сохраняется в папке \"Входящие\" и
    записывается в журнал с уникальным номером.

+ **Обработка исходящих/внутренних документов**
  
**Описание:** Пользователь может зарегистрировать исходящий документ
    с зарезервированным номером, который сохранится в соответствующей
    директории и журнале исходящих или внутренних документов.
  
**Использование:** Пользователь отправляет документ, указывает номер
    и регистрирует его.

+ **/journal** -- Просмотр журнала
  
**Описание:** Команда выводит журнал с данными о входящих, исходящих
    и внутренних документах.
  
**Использование**: Команда /journal выводит HTML страницу с журналом
    документов.

# Фронтенд (пользовательская часть)

Интерфейс пользователя представлен через Телеграм, где все
взаимодействие осуществляется с помощью команд, переданных боту. Команды
и ответы строятся на основе файлов конфигурации, хранящихся на сервере.
Пользовательские группы имеют разные привилегии и получают доступ к
разным функциям бота. Также для просмотра и управления документами
используется **HTML интерфейс** с журналами документов.

# Пошаговая инструкция по использованию

1\. **Подключение к серверу.** На облачной виртуальной машине
разворачивается облегченный дистрибутив Debian с предустановленным
Телеграм ботом и зависимостями.\
2. **Настройка файлов конфигурации.** В папках /etc/DocBot хранятся файлы с
токенами, пользователями и структурой, которые нужно настроить перед
использованием бота.\
3. **Запуск скриптов.** Для выполнения каждой функции используется
отдельный скрипт, который запускается в зависимости от команды
пользователя **(например, /get_No).**\
4. **Обработка файлов и регистрация.** Бот автоматически регистрирует
входящие и исходящие документы в журналах, сохраняя их в структуре каталогов файловой системы.\
5. **Использование журналов.** Пользователи могут запрашивать журналы с
помощью команды /journal и получать HTML страницы с данными.

## /help -- Справка (Расширенное описание)

**Дополненное описание:** Команда предназначена для вызова справочной
информации, специфичной для каждого пользователя, в зависимости от его
группы. Текст справки для каждой группы пользователей хранится в файле
manual_USERGROUPNAME. Это позволяет предоставлять персонализированную
информацию для каждой группы, например, инструкции для бухгалтерии,
команды Техцентра и т.д.

**Дополнительные возможности:**

-   \- Возможность обновления справки в реальном времени при изменениях
    в **manual_USERGROUPNAME.**

-   \- Поддержка различных языков для мультиязычных групп пользователей.

## /get_No -- Получить исходящий номер (Расширенное описание)

**Дополненное описание:** Скрипт генерирует и возвращает следующий
свободный исходящий номер для документа. Номер фиксируется в журнале и
резервируется за пользователем для последующего использования при
регистрации документа. Это позволяет отслеживать все исходящие
документы.

**Дополнительные возможности:**

-   \- Автоматическая проверка зарезервированных номеров для каждого
    пользователя.

-   \- Возможность восстановления предыдущих номеров в случае ошибок или
    отмены операции.

## Событие: отправка документа (pdf или JPEG) (Расширенное описание)

**Дополненное описание:** Этот скрипт отвечает за обработку всех
загружаемых документов в формате PDF или JPEG. Бот инициирует диалог с
пользователем, задавая серию вопросов на основе структуры, заданной в
файле **structure.conf.** Это позволяет корректно классифицировать
документы и сохранять их в соответствующих папках.

**Дополнительные возможности:**

-   \- Поддержка других форматов файлов, таких как **DOCX, XLSX.**

-   \- Автоматическое преобразование изображений в **PDF** для
    унификации форматов документов.

## Обработка входящих документов (Расширенное описание)

**Дополненное описание:** Скрипт автоматически присваивает порядковый
номер входящему документу, который затем сохраняется на сервере.
Информация о документе фиксируется в журнале входящих документов,
включая данные о пользователе, который загрузил документ.

**Дополнительные возможности:**

-   \- Уведомление о получении нового документа для ответственных лиц.

-   \- Возможность ручного редактирования записи о документе для
    внесения изменений.

## Обработка исходящих/внутренних документов (Расширенное описание)

**Дополненное описание:** Пользователь может зарегистрировать исходящий
или внутренний документ с использованием ранее полученного
зарезервированного номера. Скрипт проверяет наличие свободных номеров,
если пользователю нужно зарезервировать новый номер для документа.

**Дополнительные возможности:**

-   \- Возможность пакетной загрузки и регистрации нескольких документов
    одновременно.

-   \- Поддержка подписания исходящих документов цифровыми подписями.

## /journal -- Просмотр журнала (Расширенное описание)

**Дополненное описание:** Скрипт выводит журнал регистрации всех
документов в формате **HTML.** В журнале отображаются входящие,
исходящие и внутренние документы с полной информацией: номер документа,
дата, имя пользователя, ссылка на документ, комментарий и статус
обработки.

**Дополнительные возможности:**

-   \- Возможность экспорта журнала в **Excel** или **PDF** для
    архивирования.

-   \- Фильтрация документов по типу (входящие, исходящие, внутренние),
    дате и ответственным лицам.

**Дополнительные атрибуты и детали**

**Атрибуты**

**Входящий номер и дата регистрации:** Присваиваются системой в формате
1ПП-211/24, где 1ПП --- индекс председателя правления или руководителя,
211 --- порядковый номер письма в системе, 24 --- год регистрации.

**Регистрационный номер и дата письма, указанные контрагентом:**
Опционально, но желательно указывать дату.

**Отправитель:** Название организации, приславшей документ.

**Название документа:** Информативное название, отражающее суть
документа.

**Резолюция руководителя и дата резолюции:** Указание распоряжений и
сроков от руководителя.

**Дата и регистрационный номер ответного документа:** Для документов, на
которые был направлен ответ.

**Жизненный цикл документа**

**Регистрация**: Входящий документ регистрируется и передается
руководителю.

**Резолюция:** Руководитель составляет резолюцию, направляет документ
исполнителю.

**Контроль:** При необходимости назначается ответственное лицо за
контроль.

**Исполнение и ответ:** Поручение выполняется, составляется
документ-ответ и предоставляется на подпись.

**Регистрация ответа:** Документ регистрируется после подписания.

**Направление ответа:** Ответ отправляется контрагенту.

**Переписка:** Переписка продолжается до закрытия вопроса.

**Обработка исходящих/внутренних документов**

**Регистрация**: Зарезервированный номер сохраняется в журнале
документов.

**Использование**: Пользователь отправляет и регистрирует документ.

**Атрибуты:** Исх. номер и дата, исполнитель, отправитель, название
документа, ответ.

**Жизненный цикл:** Инициация, подписание, отправка, ответ и
дополнительные письма.

**Подфункции обработки документов**

**1. document\_[upload.sh](https://upload.sh/)**

Функция: Прием и сохранение загружаемых документов в временную папку.

**2. document\_[classification.sh](https://classification.sh/)**

Функция: Классификация и перемещение документа в соответствующую папку.

**3. document\_[registration.sh](https://registration.sh/)**

Функция: Присвоение уникального номера документу и его регистрация в
журнале.

**4. document\_[notification.sh](https://notification.sh/)**

Функция: Отправка уведомлений ответственным лицам о новом документе.

**Основной скрипт обработки документов**

**document\_[processor.sh](https://processor.sh/)**

Функция: Координация выполнения подфункций для загрузки, классификации,
регистрации и уведомления по документам.

*#!/bin/bash*

*\# document_processor.sh*

*\# Основной скрипт для обработки документов*

*\# Параметры*

FILE_PATH**=**\$1

*\# Вызов подфункций*

./document_upload.sh \"\$FILE_PATH\"

./document_classification.sh \"\$FILE_PATH\"

./document_registration.sh \"\$FILE_PATH\" \"входящий\" *\# Параметр
типа документа можно изменять*

./document_notification.sh \"\$FILE_PATH\" <responsible@example.com>

**Интеграция, конфигурация и структура системы для реализации
документооборота через Телеграм бот и Госключ**

1.  **Интеграция с системой Госключ**

> Интеграция должна включать полноценный процесс авторизации, обработку
> ошибок, взаимодействие с внутренними документами и проверку
> подлинности всех документов.

2.  **Перечень файлов конфигурации и структура каталогов**

> Основные файлы конфигурации включают:
>
> **config.yaml:** Параметры для взаимодействия с Госключом.
>
> **structure.conf:** Структура каталогов для хранения документов.
>
> **logging.conf:** Настройки логирования.
>
> Структура каталогов:
>
> **/var/www/goskey/logs/:** Логи взаимодействий с Госключом.
> **/var/www/goskey/documents/:** Хранение документов.
>
> **/var/www/goskey/temp/:** Временные файлы.

3.  **Перечень файлов скриптов с названиями**

**central\_[script.sh](https://script.sh/)**:Управляющий скрипт для
> координации процессов.

**webhook\_[handler.sh](https://handler.sh/)**: Обработка Webhook
запросов.

**document\_[processor.sh](https://processor.sh/):** Основной скрипт
обработки документов.

**error[\_]{.underline}[handler.sh](https://handler.sh/):** Обработка
ошибок.

4.  **Центральный управляющий скрипт и компоненты для реализации
    Webhook**

> Центральный управляющий скрипт управляет всеми процессами, мониторит
> работу скриптов и обрабатывает ошибки. Компоненты Webhook обрабатывают
> запросы от Телеграм и Госключ, обеспечивая масштабируемость и
> взаимодействие с другими элементами системы.
