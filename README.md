# Spring Cloud Example

[![Статус сборки](https://travis-ci.com/naXa777/spring-cloud-example.svg?branch=master&style=flat)](https://travis-ci.com/naXa777/spring-cloud-example)

Эта открытая площадка предназначена для изучения [Spring Cloud](http://spring-projects.ru/projects/spring-cloud/) и [Kotlin](https://kotlinlang.ru/) на примерах.

_Читать на других языках: [In English](README.en.md)_

## Вклад

&#x1F49A; Начните с известных проблем в [баг-трекере](https://github.com/naXa777/spring-cloud-example/issues).

## Описание

### Service Discovery

| Модуль           |
| :--------------: |
| discovery-server |

В Spring Cloud есть несколько способов обнаруживать сервисы:

* Spring Cloud [Consul](https://cloud.spring.io/spring-cloud-consul/)
* Spring Cloud [Zookeeper](https://cloud.spring.io/spring-cloud-zookeeper/)
* Spring Cloud [Netflix](https://cloud.spring.io/spring-cloud-netflix/)

Данный проект уделяет основное внимание последнему из них - Spring Cloud Netflix. Американский гигант потокового телевещания Netflix полностью открыл код своего микросервисного стека.

Ради простоты демонстрации настраивается только один экземпляр сервера Eureka. Поэтому он сконфигурирован таким образом, чтобы не регистрироваться среди пиров (других экземпляров сервера Eureka).
Скорей всего, вам потребуется запускать одновременно несколько серверов для обнаружения (Discovery servers) для того, чтобы гарантировать высокую доступность в продакшене. Для этого измените значения следующих свойств:

    eureka.client.register-with-eureka=true
    eureka.client.fetch-registry=true    

### Weather Service

| Модуль          |
| :-------------: |
| weather-service |

Аннотация `@EnableDiscoveryClient` используется, чтобы превратить приложение `WeatherServiceApplication` в клиента Discovery Server и заставить его зарегистрироваться в Discovery Server во время запуска.

### Client

| Модуль  |
| :-----: |
| client  |

Аннотация `@EnableDiscoveryClient` используется, чтобы превратить приложение `ClientApplication` в клиента Discovery Server.

Но клиентское приложение не регистрирует себя в Eureka, потому что нам не нужно, чтобы его кто-то обнаруживал. Поэтому свойство ниже установлено в false:

    eureka.client.register-with-eureka=false
    
## Собираем и запускаем локально

### Подготовка

Перед первой сборкой приложения необходимо предпринять несколько допольнительных шагов.

 - Первое: клонировать репозиторий.
 - Второе: определить несколько переменных окружения.
   - &#x1F4D7; _TODO_

Вы обладаете свободой выбора средства для сборки этого проекта: [Gradle](https://gradle.org/) или любимая среда разработки.
[IntelliJ IDEA](https://spring.io/guides/gs/intellij-idea/), [STS](https://stackoverflow.com/q/34214685/1429387) / [Eclipse](http://www.vogella.com/tutorials/EclipseGradle/article.html), или [NetBeans](https://netbeans.org/features/java/build-tools.html) должны справиться с этой задачей без проблем.

### Используя обёртку Gradle

    ./gradlew :discovery-server:bootRun
    ./gradlew :weather-service:bootRun
    ./gradlew :client:bootRun

### Используя IntelliJ IDEA

1. Импортируйте корневой проект (файл build.gradle) в IntelliJ IDEA.
2. Синхронизируйте настройки проекта с Gradle (первая синхронизация может запуститься автоматически после импорта, в таком случае дополнительных действий не требуется).
3. После импорта и синхронизации у вас должны были появиться несколько конфигураций, по одной для каждого модуля. Запускайте их по-порядку:
    1. DiscoveryServerApplication
    2. WeatherServiceApplication
    3. ClientApplication
    
Подсказка: убедитесь, что запускаете их на разных портах и что эти порты не заняты другими приложениями, во избежание конфликта.

## Развёртывание в облаке

&#x1F4D7; _TODO_

## Непрерывная интеграция

| [Travis CI](https://travis-ci.com/) | [![Статус сборки](https://travis-ci.com/naXa777/spring-cloud-example.svg?branch=master&style=flat)](https://travis-ci.com/naXa777/spring-cloud-example) |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Лицензия

Данный проект лицензирован на условиях [GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0.ru.html).

Неофициальный перевод текста лицензии: [Google Code Archive](https://code.google.com/archive/p/gpl3rus/wikis/LatestRelease.wiki).
