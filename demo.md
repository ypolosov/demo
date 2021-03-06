# Создание демо-приложения 'modular-project'

Целью данного мануала является научится создавать веб-приложения с компонентной структурой на языке typescript.
Результатом прохождения данного мануала является простое веб-приложение собранное из произвольного набора компонентов разных типов: компонент, набор компонентов, старонний компонент, компонент-приложение. Готовое приложение можно получить по адресу (создать репозиторий и вставить ссылку) и сверяться с ним как с эталоном в процессе прохождения мануала.

## Создание рабочей директории

* Создайте рабочую директорию
````shell
mkdir /GITS2/devkit/js/demo/modular-project
````
Для простоты в этой рабочей директории будут созданы все проекты, но в реальном приложении они могут находится в разных местах файловой системы и даже на разных удаленных машинах.

## Запуск скаффолдера
Для быстрого создания типовых проектов используется система скаффолдинга yeoman. Все типы проектов создаются с помощью скаффолдера generator-boilerplate созданного в нашей компании, который является yeoman плагином

````shell
/GITS2/tools/js/yeoman-generators/generator-boilerplate
````

* Запустите скаффолдер из рабочей директории
````shell
yo boilerplate
````

## Создание типового проекта 'компонент' (project-per-module)

В процессе разработки возникает необходимость выделения специфического функционала в отдельные пограммные единицы позволяющие повторное испольщование. Для этой цели отлично подходит тип проекта 'компонент'. Далее следуйте подсказкама или примените значения по умолчанию в скобках.

* Выбирите тип проекта 
````shell
project-per-module
````

* Укажите имя проекта 
````shell
domestic-lib
````

* Укажите имя фасадного файла модуля 
````shell
Domestic
````

* Откажитесь от установки npm install (вы сможите это сделать позже)
````shell
false
````

* Откажитесь от установки bower install (вы сможите это сделать позже)
````shell
false
````

* Откажитесь от генерацией скриптов (вы сможите это сделать позже)
````shell
false
````

Результатом окажется прокет 'domestic-lib' с тремя подпроектами, которые в дальнейшем должны быть добавлены в отдельные git репозитории

* [dev](#dev) - репозиторий разработки typescript модуля
* [dist](#dist) - репозиторий публикации typescript модуля в продакшен для использования в качестве зависимости в других модулях
* [test](#test) - репозиторий тестирования typescript модуля

Каждый подпроект снабжен сответствующими конфигурационными файлами и необходимым минимумом исходников для сборки

## Работа в подпроекте разработки компонента (dev)

Непосредственно разработка компонента происходит в подпроекте (dev)

* Переместитесь в подпроект dev проекта domestic-lib
````shell
cd /GITS2/devkit/js/demo/modular-project/domestic-lib/dev
````

### Установка средств поддержки времени разработки

В качестве таск-раннера в экосистеме используется grunt. Также в компании разработан grunt-project-builder плагин для сборки и зауска компонентов и тестов для них. 

````shell
/GITS2/tools/js/grunt-plugins/grunt-project-builder
````

Перед началом работы с любым из подпроектов необходимо установить средства поддержки времени разработки: штатного инструмента grunt-project-builder и других сторонних grunt плагинов если необходимая функциональновть не предусмотрена в штатном инструменте. grunt-project-builder может быть расширен при необходимости. Все средства поддержки времени разработки являются npm пакетами. Для указания установки необходимых средств разработки в каждом подпроекте существует конфигурационный файл package.json. Например:

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/package.json
````

* Установите средства поддержки времени разработки
````shell
npm install
````

Установленные средства поддержки времени разработки появятся в следующей директории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/node_modules
````

### Установка компонентов-зависимостей для разрабатуемого модуля

Разрабатуемый компонент может использовать или расширять другие комопненты, таким образом он нуждается в указании зависимостей на соответствующие компоненты. Для обеспечения дерева зависимостей между компонентами используется стандарт веб-компонента bower. Все создаваемые и используемые в качестве зависимостей компоненты должны являться bower компонентами. Для указания установки необходимых компонентов-зависимостей в каждом подпроекте dev существует конфигурационный файл bower.json, который должен содержать только имя и перечень зависимостей. Например:

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/bower.json
````

* Установите компоненты-зависимости
````shell
bower install
````

Установленные компоненты-зависимости (если указаны) появятся в следующей директории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/bower_components
````

### Генерация скриптов частичной автоматизации процесса разработки

Для систематизации и упрощеия процесса разработки система сборки проектов предоставляет возможность генерации скриптов частичной автоматизации. Система сборки выполняет генерацию скриптов по первому обращению или в результате выполнения команды по умолчанию

* Сгенерите скрипты частичной автоматизации из подпроекта dev
````shell
grunt
````
или
````shell
grunt default
````

Cгенеренные скрипты появятся в соответствующей поддиректории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/scripts
````

* [build.cmd](#) - сборка компонента
* [publish.cmd](#) - публикация компонента
* [build_and_publish.cmd](#) - сборка и публикация компонента
* [install-npm.cmd](#) - установка средств поддержки времени разработки
* [install-bower.cmd](#) - установка компонентов-зависимостей для разрабатуемого модуля
* [scripts.cmd](#) - регенерация скриптов частичной автоматизации процесса разработки
* [link-bower.cmd](#) - создание симлинка на разрабатываемый компонент для поддержки времени разработки

### Сборка компонента

Упрощенно сборка компонента включает следующие этапы

1. конфигурация проекта и настройка зависимостей на используемые модули
2. компиляция typescript в javascript
3. генерация или загрузка с внешнего ресурса TypeScript definition файлов (*.d.ts)
4. автоматическое постороение графа зависимостей в виде AMD модулей
5. конкатанация AMD модулей без внешних зависимостей в один итоговый файл (*.js)

* Собирите компонент выполнив команду из подпроекта разработки компонента (dev)
````shell
grunt build
````
или запуств соответствующий скрипт
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/scripts/build.cmd
````

Результат сборки появятся в соответствующей поддиректории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/out
````

* [DomesticModule.d.ts](#) - главный файл реализации компонента на языке javascript 
* [DomesticModule.js](#) - главный файл публичного API компонента в формате описания типов на языке typescript

### Тестирование подсистем компонента в течении разработки

В процессе разработки возникает необходимость тестирования отдельных подсистем разрабатываемого компонента. Данный вид тестирования реализован с использованием тест-раннера karma и тест-фреймворка jasmine. Тесты описаны в файлах вида *Spec.ts и распалагаются в поддиректории test (на одном уровне с api и impl) произвольно выделенной подсистемы компонента. Например
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/src/api/Domestic.ts - API подсистемы
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/src/impl/DomesticImpl.ts - реализация подсистемы
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/src/test/DomesticSpec.ts - тест подистемы
````

#### Запуск spec-тестов

* Запустите spec-тесты выполнив команду из подпроекта dev
````shell
grunt karma
````

В результате среда karma откроет браузер и выполнит spec-тесты. В консоли должно быть нечто похожее
````shell
Chrome 46.0.2490 (Windows 7 0.0.0) LOG: 'DomesticImpl.constructor was called !!!'
Chrome 46.0.2490 (Windows 7 0.0.0): Executed 1 of 1 SUCCESS (0.054 secs / 0.002 secs)
````

#### Настройка списка запускаемых spec-тестов

Список запускаемых spec-тестов можно настроить в конфигурационном файле gruntfile.js
````shell
specs: {
    files: [
        "test/DomesticSpec"
    ]
}
````

### Публикация компонента

Готовый компонент должен быть доступен для использования из подпроекта dist. Для этого результаты сбрки должены быть скопированы туда из подпроекта разработки (dev)

* Опубликуйте результат сборки компонента выполнив команду из подпроекта разработки
````shell
grunt publish
````
или запуств соответствующий скрипт
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/scripts/publish.cmd
````

## Работа в подпроекте публикации компонента (dist)

Готовым к использованию опубликованым компонентом является bower веб-компонент состоящий из следующих ресурсов

* [DomesticModule.d.ts](#) - главный файл реализации компонента на языке javascript 
* [DomesticModule.js](#) - главный файл публичного API компонента в формате описания типов на языке typescript
* [bower.json](#) - конфигурационный файл для bower компонентов ( используется для указания зависимостей на другие bower компоненты )

### Настройка публикуемого компонента

Для настройки публикуемого компонента используется конфигурационный файл bower.json в корне подпроекта dist. Например
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dist/bower.json
````

ВАЖНО! В отличие от одноименного конфигурационного файла из подпроекта dev, в подпроекте dist он содержит исчерпывающую информацию о компоненте, а не только перечень зависимостей

### Виды публикаций компонента

Как только вы опубликовали компонент он может быть использован двумя разными способами

#### Релиз-публикация

Для релиз публикации компонента необходимо создать git репозиторий на сервере компании на основе подпроекта dist и залить в него ресурсы компонента. После этого релиз данного компонента будет доступен для использования в качастве зависимости в bower.json других компонентов по ссылке вида

````shell
"DomesticModule": "git@git.providesupport.com:devkit/js/demo/modular-project/domestic-lib/dist"
````

#### Публикация поддержки времени разработки

В процессе разработки нескольких зависимых компонентов, каждый из них может интенсивно изменятся и указание зависимостей на них по средством релиз-публикации затрудняет разработку. Поэтому специально для упращения разработки используется другой способ по средством создания симлинка на локальной машине под контролем системы bower, что позволяет учитывать изменения зависимых компонентов 'на лету'  

##### Создание bower симлинка из публикуемого компонента

* Создайте bower симлинк на базе разрабатуемого компонента, выполнив команду из подпроекта dist
````shell
bower link
````
или запуств соответствующий скрипт
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/dev/scripts/link-bower.cmd
````

Результатом должен стать симлинк 'domestic-lib', указывающий на подпроект dist, в следующей директории 

````shell
%USERPROFILE%\AppData\Local\bower\data\links
````

##### Использование bower симлинка в качестве зависимости на компонент

* Создайте зависимость на публикуемый компонент через bower симлинк, выполнив команду из подпроекта (dev, test или app) зависимого компонента
````shell
bower link domestic-lib
````

## Работа в подпроекте тестирования компонента (test)

Подпроект test позволяет тестировать разрабатываемый компонент как 'черный ящик' строго через публичное API, по средством простого тестового приложения, с линейным произвольным набором тестов с выводом в лог на страницу или консоль браузера. Такие теств удобны для периодического тестирования компонента или подтверждения его актуального работоспособного состояния

Тесты реализуются на языке typescript. Результатом сборки подпроекта test также является bower компонент, который в качестве зависимости имеет ссылку на разрабатываемый компонент из подпроекта dev

* Перейдите в подпроект test
````shell
cd /GITS2/devkit/js/demo/modular-project/domestic-lib/test
````

### Установка средств поддержки времени разработки

Для указания установки необходимых средств разработки в подпроекте существует конфигурационный файл package.json, аналогичный одноименному файлу из под проекта dev. Например:

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/package.json
````

* Установите средства поддержки времени разработки
````shell
npm install
````

Установленные средства поддержки времени разработки появятся в следующей директории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/node_modules
````

### Установка компонентов-зависимостей для разрабатуемого модуля

Для указания установки необходимых компонентов-зависимостей в подпроекте test существует конфигурационный файл bower.json, который должен содержать только имя и перечень зависимостей. Например:

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/bower.json
````

* Установите компоненты-зависимости
````shell
bower install
````

Для подгрузки тест-компонента в тестовом приложении используется ссылка на релиз-публикацию AMD-лоадера 'requirejs', зависимость на него указана в bower.json в блоке devDependencies, так как он не является прямой зависимостью компонента, а используется лишь как вспомогательный инструмент. 

Установленные компоненты-зависимости появятся в следующей директории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/bower_components
````


### Генерация скриптов частичной автоматизации процесса разработки

 Система сборки выполняет генерацию скриптов по первому обращению или в результате выполнения команды по умолчанию

* Сгенерите скрипты частичной автоматизации из подпроекта test
````shell
grunt
````
или
````shell
grunt default
````

Cгенеренные скрипты появятся в соответствующей поддиректории

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/scripts
````

* [build_integ_debug_test.cmd](#) - сборка тест-компонента в debug версии
* [build_integ_release_test.cmd](#) - сборка тест-компонента в release версии
* [run_integ_test.cmd](#) - запуск тестового веб-приложения
* [build_and_run_integ_debug_test.cmd](#) - сборка тест-компонента и запуск тестового веб-приложения в debug версии
* [build_and_run_integ_release_test.cmd](#) - сборка тест-компонента и запуск тестового веб-приложения в release версии
* [clean-bower.cmd](#) - очистка bower_components директории, полезно выполнять при чередовании debug и release тест-сборок
* [install-npm.cmd](#) - установка средств поддержки времени разработки
* [install-bower.cmd](#) - установка компонентов-зависимостей для разрабатуемого модуля
* [scripts.cmd](#) - регенерация скриптов частичной автоматизации процесса разработки

### Установка зависимости на тестируемый компонет через bower симлинк

* Выполните команду из подпроекта test (симлинк %USERPROFILE%\AppData\Local\bower\data\links\domestic-lib должен существовать)
````shell
bower link domestic-lib
````

В результате в подпроекте должен появится симлинк на тестируемый компонент (возможна ошибка во время выполнения 'ENOTINS Package domestic-lib is not installed')

````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/bower_components/domestic-lib
````

### Сборка тест-компонента

* Соберите тест-компонент запустив скрипт
````shell
build_integ_debug_test.cmd
````

В результате должно быть создано веб-приложение
````shell
/GITS2/devkit/js/demo/modular-project/domestic-lib/test/bower_components/domestic-lib/test/integ/www
````

* [index.html](#) - главный файл тестового веб-приложения 
* [test.css](#) - минимальный css (если тестируемый компонент содержит ресурсы (картинки, шрифты, стили) они включаются сюда)
* [test.js](#) - итоговый js файл, содержит тестируемый компонент со всеми внешними зависимостями и AMD-загрузчик 'requirejs'

### Запуск тестового приложения 

* Запустите тесовое приложение выполнив скрипт
````shell
run_integ_test.cmd
````

В результате в браузере откроется тестовое веб-приложение. На странице должна быть надпись
````shell
Hello scaffolded DomesticModule!
````

ВАЖНО! Для остановки веб-сервера жмем CTRL + C
