# Статический анализ проекта 🐞

# Findbugs

Разработка проектов сопровождается различными ошибками. Все ошибки очень тяжело сразу предусмотреть особенно если вы не очень хорошо знакомы с инструментом или на проекте есть молодые разработчики. Для анализа некоторых ошибок есть специальный класс инструментов - статический анализаторы.

Для Java разработки есть популярный инструмент [Spotbugs](https://spotbugs.github.io) (бывший [findbugs](http://findbugs.sourceforge.net)). 

## Пример

Давайте склонируем проект при помощи команды 

```bash
git clone https://github.com/mebr0/integrated-twitter
```

Удостоверьтесь, что проект использует последнюю версию Gradle. И привидите содержимое файла в следующий вид `gradle/wrapper/gradle-wrapper.properties`.

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-7.1.1-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

Далее нам необходимо добавить плагин Spotbugs в Gradle согласно [документации](https://plugins.gradle.org/plugin/com.github.spotbugs) и сконфигурировать плагин в файле **build.gradle** Добавив следующие строки:

```java
spotbugs {
    toolVersion = '4.3.0'
}

spotbugsMain {
    reports {
        html {
            enabled = true
        }
    }
}
```

Мы добавили в проект `spotbugs` версии - `4.3.0`. Для запуска анализа в терминале выполните следующую команду 

```bash
./gradlew spotbugsMain
```

В ходе работы будет сгенерирован HTML отчет:

```
> A failure occurred while executing com.github.spotbugs.snom.internal.SpotBugsRunnerForWorker$SpotBugsExecutor
   > 2 SpotBugs violations were found. See the report at: file:///private/tmp/integrated-twitter/build/reports/spotbugs/main.html

* Try:
Run with --stacktrace option to get the stack trace. Run with --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

See https://docs.gradle.org/7.1.1/userguide/command_line_interface.html#sec:command_line_warnings

BUILD FAILED in 22s
4 actionable tasks: 2 executed, 2 up-to-date
Watched directory hierarchies: [/private/tmp/integrated-twitter]

```

Откройте отчет в браузере и распишите на какую ошибку указывает отчет. 

Так же можно воспользоваться [системой фильтров](https://spotbugs.readthedocs.io/en/latest/filter.html). Давайте попробуем сделать фильтр и добиться игнорирования ошибок. 

Давайте исключим ошибки которые были выявлена на этапе анализа и сделаем отчет с 0 количеством ошибок. Для этого относительно корня проекта создайте файл по следующему пути `config/spotbugs/ignore/exclude.xml` и задайте ему следующее содержимое.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<FindBugsFilter>
    <Match>
        <Package name="com.mebr0.dto" />
        <Bug pattern="EI_EXPOSE_REP"/>
    </Match>

    <Match>
        <Package name="com.mebr0.dto" />
        <Bug pattern="EI_EXPOSE_REP2"/>
    </Match>
</FindBugsFilter>
```

И обновите задачи `Spotbugs` в Gradle добавив файл с исключением 


```groovy
spotbugs {
    toolVersion = '4.3.0'
    excludeFilter = file("config/spotbugs/ignore/exclude.xml")
}

spotbugsMain {
    reports {
        html {
            enabled = true
        }
    }
}
```

И затем выполните команду анализа снова `./gradlew spotbugsMain`. В результате вы должны получит чистый отчет и успешное завершение анализа.

```bash
> Task :spotbugsMain
Caching disabled for task ':spotbugsMain' because:
  Build cache is disabled
Task ':spotbugsMain' is not up-to-date because:
  Task has failed previously.
Running SpotBugs by Gradle process-isolated Worker...
SpotBugs 4.3.0
:spotbugsMain (Thread[Execution worker for ':',5,main]) completed. Took 1.365 secs.

Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

See https://docs.gradle.org/7.1.1/userguide/command_line_interface.html#sec:command_line_warnings

BUILD SUCCESSFUL in 3s
4 actionable tasks: 1 executed, 3 up-to-date
Watched directory hierarchies: [/private/tmp/integrated-twitter]
```

Там образом мы получили базовые навыки настройки инструмента `Findbugs`.

## Задание

- проделайте все операции для настройки `findbugs` на тестовом проекте
- сделайте краткое описание о инструменте `findbugs`
- опишите какие типы ошибок может помочь решить данный анализатор
- попробуйте отключить файл фильтр и исправит ошибки которые имеет анализатор
- разберитесь с настройкой строгости проверки `findbugs`. В этом вам помогут две ссылки
    - [effort](https://spotbugs.readthedocs.io/en/stable/effort.html)
    - [gradle plugin](https://github.com/spotbugs/spotbugs-gradle-plugin#readme)
- разберитесь с подключением [spotbugs в Idea](https://plugins.jetbrains.com/plugin/14014-spotbugs) и опишите возможности и преимущества плагина