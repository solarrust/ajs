# AJS. Рабочее окружение

###### tags: `netology` `advanced js`

---

## План занятия

* npm
* live-server
* ESLint
* Babel

---

## Рабочее окружение

Современная разработка на JavaScript (далее - JS) представляет из себя достаточно комплексный процесс, и одной из ключевых составляющих этого процесса является настройка рабочего окружения.

---

## Рабочее окружение

Под рабочим окружением мы будем понимать не только (и не столько) настройку редактора кода или IDE, сколько использование инструментов, не завязанных на IDE и облегчающих:
* разработку
* тестирование
* соблюдение правил

---

## IDE и редактор кода

Для большинства программистов - выбор IDE является сугубо личным делом, поэтому мы будем настраивать рабочее окружение независимо от IDE.

---

## HTTP Server

Рассмотрим следующую задачу: нам нужно установить локальный http-сервер, для того, чтобы разрабатывать, тестировать и отлаживать наше приложение.

Мы, конечно, можем загуглить и найти пару подходящих решений - от тяжеловесов вроде Apache и Nginx до более-менее легковесных решений.

Но, может, есть способ попроще?

---

--- 

## Почему нельзя просто кодить в файлике?

Можно, но нужно привыкать использовать профессиональные инструменты. 

Если вы будете работать в команде, то вас банально "не поймут" и придётся очень быстро переучиваться.

---

## npm

---

## npm

[npm](https://www.npmjs.com) - менеджер пакетов для JS, реестр готовых пакетов и утилита командной строки в одном флаконе.

Стандарт де-факто в мире JS для организации рабочего окружения.

На сегодняшний день содержит более 800 000 готовых пакетов.

---

## npm

Для iPhone есть AppStore, для Android - Google Play, а для JS - npm.

![](https://i.imgur.com/McKybpJ.png)

---

## Установка

npm уже входит в состав [Node.js](https://nodejs.org), который вы должы были установить в качестве предварительных требований к нашему курсу.

Чтобы проверить, что npm действительно установлен, выполните команду в терминале:
```shell
$ npm -v
6.5.0
```

Если у вас версия 6.5.0 или более новая, то всё ок.

---

## Использование терминала

* Есть ли у вас проблемы с использованием терминала?
* Прочитали ли вы мануал по его использованию?
* Есть ли вопросы?

---

## HTTP Server

Вернёмся к нашей задаче. Установим HTTP Server с использованием npm:
```shell
$ npm install --global http-server
```

Команда `npm install [--global] <package-name>` позволяет нам устаналивать любой пакет из реестра https://npmjs.com

Флаг `--global` указывает, что пакет устанавливается глобально (global mode), т.е. будет доступен в рамках всей системы (или текущего пользователя ОС).

---

## Справка npm

```shell
$ npm help
$ npm help <command>
$ npm <command> --help
```

Полный перечень всех команд с описанием представлен на веб-странице: https://docs.npmjs.com/cli-documentation/

---


## Запуск HTTP Server'а

Откроем в терминале каталог нашего проекта и запустим http-server:
```shell
$ cd src
$ http-server
Starting up http-server, serving ./
Available on:
  http://127.0.0.1:8080
Hit CTRL-C to stop the server
```

Остаётся открыть браузер с адресом http://localhost:8080


:::info
В VSCode уже встроен терминал, можно его открыть сочетанием клавиш ``Ctrl + ` `` (Windows/Linux), `` ^ + ` `` (Mac).

:::

---

## Справка

Большинство пакетов, поставляемых через npm содержат встроенную справку, которую достаточно легко вызвать, например:

```shell
$ http-server --help
usage: http-server [path] [options]

options:
  -p           Port to use [8080]
  -a           Address to use [0.0.0.0]
  -d           Show directory listings [true]
  -i           Display autoIndex [true]
  -g --gzip    Serve gzip files when possible [false]
  -e --ext     Default file extension if none supplied [none]
  -s --silent  Suppress log messages from output
  --cors[=headers]   Enable CORS via the "Access-Control-Allow-Origin" header
                     Optionally provide CORS headers list separated by commas
  -o [path]    Open browser window after starting the server
  -c           Cache time (max-age) in seconds [3600], e.g. -c10 for 10 seconds.
               To disable caching, use -c-1.
...
```

---

## Репозиторий пакета

Одной командой мы получили готовый и легковесный http-server с большим набором опций.

Кроме того, мы можем даже сразу открыть страницу GitHub-проекта:
```shell
$ npm repo http-server
```

---

## Минусы

Плюсов достаточно много. А минусы?

Минусы такого подхода:
1. Засоряется "глобальная область видимости" (global mode)
2. Как мы будем работать в команде (писать всем инструкции)?

Можно ли настраивать и устанавливать пакеты только для текущего проекта?

---

## Пакет

В терминах npm - пакет это любой каталог* ([более подробно](https://docs.npmjs.com/about-packages-and-modules#about-packages)), содержащий файл `package.json`.

Для пакета можно настроить зависимости - пакеты, которые нужны для функционирования (зависимости) или для разработки, тестирования (dev-зависимости).

Кроме того, можно вынести ключевые команды в скрипты.

Разберёмся по шагам.

---

## Инициализация пакета

Выполним в нашем проекте (не в каталоге `src`, а в корне нашего проекта):
```shell
$ npm init
```

Запустится конфигуратор пакета, который задаст вам ряд вопросов, после чего сгенерируется файл `package.json`.

:::warning
Важно: старайтесь создавать пакеты в каталогах, которые не содержат в пути пробелов, спец.символов, кириллицы и т.д.
::: 

---

## Ключевые поля Package.json

* name - название пакета
* version - версия (в соответствии с https://semver.org)
* scripts - скрипты (удобные сокращения для команд)

И два раздела, которых у нас пока нет:
* dependencies - зависимости, необходимые для функционирования пакета
* devDependencies - зависимости, необходимые для разработки и (или) тестирования пакета

---

## Установка пакета локально

Зависимости, устанавливаются с помощью команды `npm install`:
```shell
$ npm install [--save-dev] <package-name>
```

Флаг `--save-dev` означает, что зависимость нужна только для разработки и тестирования. Поскольку http-server нам нужен как раз для этих целей, то он является dev-зависимостью:

```shell
$ npm install --save-dev http-server
```

---

## Dev Dependencies

В результате выполнения команды в нашем проекте создался каталог `node_modules` и в `package.json` появилась секция `devDependencies`:
```json
  "devDependencies": {
    "http-server": "^0.11.1"
  }
```

Посмотреть список локально установленных пакетов мы можем с помощью команды:
```shell
$ npm list
```

---

## Scripts

Теперь возникает вопрос, как же запустить http-server?

Сам исполняемый файл хранится в каталоге `node_modules/.bin/http-server`, чтобы оттуда его запустить, мы можем прописать его в секцию scripts следующим образом:

```json
  "scripts": {
    "serve": "http-server src",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

И в командной строке просто запускать команду:
```shell
$ npm run serve
```

---

## Scripts

В скрипты можно прописывать любые команды, которые могут выполнится в терминале. Таким образом, это удобный способ:
1. Дать псевдоним длинной команде
2. Определить набор стандартных команд для вашего проекта

---

## Стандартные имена

Ряд имён в скриптах стандартизирован и позволяет опускать ключевое слово `run`. Например, изменим секцию `scripts`:
```json
  "scripts": {
    "start": "http-server src",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
```

```shell
$ npm start
```

---

## Список стандартных имён

* start
* stop
* test
* restart

Полный список приведён на странице https://docs.npmjs.com/misc/scripts.html#description

---

## Поиск пакета

С http-server всё достаточно хорошо, но для разработки нужен более мощный инструмент, который бы содержал в себе функцию автоматической перезагрузки страницы при изменении хотя бы одного файла.

Это называется ==live reload==.

Поищем такой инструмент через npm:
```shell
$ npm search --long live reload
```

Какую команду нужно использовать для установки?

---

## Установка live-server

Среди прочих мы увидим live-server, установим его командой:
```shell
$ npm install --save-dev live-server
```

И заменим http-server на live-server в скрипте `start`.

Теперь любое изменение файлов в каталоге `src` приводит к перезагрузке страницы в браузере - достаточно удобно.

---

## Удаление пакетов

Теперь у нас установлены http-server локально и глобально, но они нам уже не нужны. Как их удалить?

Удалим глобально установленный http-server:
```shell
$ npm uninstall --global http-server
$ npm list --global
```

Удалим локально установленный http-server:
```shell
$ npm unistall http-server
$ npm list
```

---

## Git

Возникает вопрос, какие из созданных npm файлов и каталогов стоит хранить в Git?

Хранить в Git:
* package.json
* package-lock.json

Не хранить в Git: `node_modules`

Все зависимости из `node_modules` легко восстанавливаются командой:
```shell
$ npm install
```

---

## .gitignore

Лучше использовать готовый `.gitignore`, собранный сообществом: https://github.com/github/gitignore/blob/master/Node.gitignore

---

## Стандарты кодирования

---

## Командная разработка

Стиль кодирования - одна из самых больных тем при разработке проектов. Здесь всё так же, как с IDE - у каждого свой вкус, но если мы хотим получить хороший продукт, нужно установить правила и придерживаться их.

Посмотрим, помогут ли инструменты, распространяемые через npm нам чем-то помочь.

---

## ESLint

[ESLint](https://eslint.org) - представитель инструментов lint'инга в мире JS (инструменты, отслеживающие стиль кодирования и типичные ошибки).

Установим его с помощью npm:
```shell
$ npm install --save-dev eslint
```

:::info
Посмотреть на работу ESLint в live-режиме: https://eslint.org/demo/
:::

---

## Формируем набор правил

npm включает в себя утилиту [npx](https://www.npmjs.com/package/npx), позволяющую запускать команды из `node_modules/.bin` либо выполняя временную установку.

Поскольку набор правил мы формируем только один раз, воспользуемся ею:

```shell
$ npx eslint --init
```

Будет запущен конфигуратор, предлагающий выбрать стиль (в том числе, среди популярных). Выберем стиль [Airbnb](https://github.com/airbnb/javascript) и формат JSON в качестве конфигурационного файла (при этом будет предложено установить доп.зависимость eslint-config-airbnb-base).

:::info
Изучите самостоятельно [styleguide airbnb](https://github.com/airbnb/javascript).
:::

---

## .eslintrc.json

ESLint будет хранить свои настройки в файле `.eslintrc.json`:

```json
{
    "extends": "airbnb-base"
    "env": {
        "es6": true,
        "browser" true
    }
}
```

---

## lint script

Создадим отдельный скрипт `lint`, который и будет запускать ESLint в соответствии с установленными настройками:
```json
  "scripts": {
    "start": "live-server src",
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint ."
  },
```

Поскольку имя `lint` не относится к стандартным, нам необходимо будет запускать его следующим образом:
```shell
$ npm run lint
```
![](https://i.imgur.com/hkTvx5k.png)

---

## Fix от ESLint

ESLint предлагает нам передать ключ `--fix` для того, чтобы исправить проблемы. Чтобы в npm-скрипт передать этот флаг, нам нужно воспользоваться специальным синтаксисом:
```shell
$ npm run lint -- --fix
```

Т.е. флаги команды следует передавать после `--`.

:::warning
Лучше исправить ошибки и warning'и ESLint'а вручную, чем доверяться автоматическому фиксатору.
:::

---

## Lint'инг

Итого: мы с вами с помощью инструмента ESLint получили возможность для нашего проекта определять стиль кодирования и проверять его с помощью npm. Но как сделать так, чтобы ошибки стиля автоматически подсвечивались в редакторе кода?

Придётся устанавливать плагин для редактора. Для VSCode необходимо зайти на вкладку расширений и установить плагин ESLint от Dirk Baeumer. После этого нам прямо в редакторе будут подсвечиваться подсказки от ESLint в соответствии с установленной конфигурацией.

Для других редакторов/IDE - аналогично.

---

## Поддержка стандартов ECMAScript

---

## ECMAScript

На прошлой лекции мы с вами рассмотрели важность стандартов ECMAScript и знания того, какая версия стандарта используется на нашем проекте.

Представим ситуацию: мы пишем библиотеку, которую хотим использовать в нескольких разных проектах. Как нам в этом случае поступить с поддержкой стандартов различных версий?

---

## ECMAScript

Варианты решения:
1. Выбрать самый старый и писать на нём (тогда не получится использовать новые возможности)
2. Выбрать самый новый и не думать о совместимости (тогда придётся переписывать)
3. Одновременно поддерживать несколько версий (трудоёмко)

---

## Babel

Проект [Babel](https://babeljs.io) предлагает альтернативное решение: транспайлер - инструмент, преобразующий код из одной версии стандарта в другую (более старую).

Т.е. мы можем использовать большинство* (если они поддерживаются транспайлером) новых возможностей языка и получать код, написанный в режиме совместимости с нужной нам версией.

Давайте посмотрим на это.

---

## Установка

```shell
$ npm install --save-dev @babel/core @babel/cli @babel/preset-env
```

:::info
Посмотреть на работу Babel в live-режиме: https://babeljs.io/en/repl.html
:::

--- 

## Формирование набора правил 

В отличие от ESLint, для Babel конфигурационный файл необходимо создать вручную (`.babelrc`):

```json
{
  "presets": ["@babel/preset-env"]
}
```

После чего в `scripts` прописать:
```json
  "scripts": {
    "start": "live-server src",
    "test": "echo \"Error: no test specified\" && exit 1",
    "lint": "eslint .",
    "build": "babel src -d dist"
  },
```

---

## Транспайлинг

Запуск транспайлинга:
```shell
npm run build
```

В результате выполнения этой команды создастся файл `dist/js/index.js`, в котором будет только совместимый [с текущей средой выполнения и настройками авторов Babel'а](https://babeljs.io/docs/en/babel-preset-env) код.

---

## Browserslist

Файл с именем `.browserslistrc` - позволяет установить, поддержку каких браузеров (окружений) необходимо обеспечивать, исходя из статистики caniuse.com

```
# Browsers that we support

last 1 version
> 1%
maintained node versions
not dead
```

---

## Babel & ESLint

ESLint на данный момент анализирует все файлы в нашем проекте (включая те, что в каталоге `dist`).

Изменим настройки ESLint так, чтобы каталог `dist` игнорировался полностью. Для этого нам нужен файл `.eslintignore`:
```
dist
```

Таким образом, ESLint будет игнорировать данный каталог, как и плагины для редакторов/IDE.

---

## Зачем это всё?

Это инфраструктура современного JS. В дальнейшем, с каким бы вы проектом или фреймворком (Angular, Vue, React) не сталкивались с большой долей вероятности он будет использовать эту инфраструктуру.

---

## Итоги

---

## Итоги

Сегодня мы с вами рассмотрели достаточно много важных вещей, а именно:
1. npm - позволяет упростить работу с проектами и зависимостями
2. live-server - позволяет упростить разработку и отладку в браузере
3. eslint - позволяет искать ошибки и соблюдать стиль кодирования
4. babel - решает проблему поддержки предыдущих версий стандарта

В следующих лекциях мы будем продолжать использовать эти инструменты

---

## Важно

Начиная с сегодняшнего дня во всех домашних заданиях мы будем требовать от вас:
1. Использования npm при формировании проекта ДЗ
2. Соответсвия ESLint набору правил Airbnb на уровне отсутствия ошибок (error)

---

## Полезные ссылки

* [Документация npm](https://docs.npmjs.com)
* [Документация live-server](https://www.npmjs.com/package/live-server)
* [Документация ESLint](https://eslint.org/docs/user-guide/getting-started)
* [Документация Babel](https://babeljs.io/docs/en/)
* [Документация Browserslist](https://github.com/browserslist/browserslist)