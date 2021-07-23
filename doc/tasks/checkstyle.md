# Валидация качества кода на проекте

## Checkstyle

TODO: Добавить описание о инструменте

## Задание

- почитать про инструмент https://checkstyle.sourceforge.io
- склонировать репозиторий https://github.com/mebr0/integrated-twitter
- создать конфигурационный файл checkstyle и добавить google code style
- проанализировать проект

## Пример

Давайте склонируем проект при помощи команды 

```bash
git clone https://github.com/mebr0/integrated-twitter
```

> для полноценного изучения работы с git рекомендуется изучить официальную документацию на сайте [git-scm.com](https://git-scm.com) и пройти интерактивное обучение [learngitbranching.js.org](https://learngitbranching.js.org/?locale=ru_RU).

Удостоверьтесь, что проект использует последнюю версию Gradle. И привидите содержимое файла в следующий вид `gradle/wrapper/gradle-wrapper.properties`.

```properties
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-7.1.1-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

Далее ознакомьтесь с документацией [Checkstyle](https://checkstyle.sourceforge.io). Затем перейдите в репозиторий с проектом и создайте файл в 2 последовательных дирректориях `config/checkstyle/checkstyle.xml`.

Заполните его следующим контентом 

```xml
<?xml version="1.0"?>
<!DOCTYPE module PUBLIC
        "-//Checkstyle//DTD Checkstyle Configuration 1.3//EN"
        "https://checkstyle.org/dtds/configuration_1_3.dtd">

<!--
  Checkstyle configuration that checks the sun coding conventions from:
    - the Java Language Specification at
      https://docs.oracle.com/javase/specs/jls/se11/html/index.html
    - the Sun Code Conventions at https://www.oracle.com/java/technologies/javase/codeconventions-contents.html
    - the Javadoc guidelines at
      https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html
    - the JDK Api documentation https://docs.oracle.com/en/java/javase/11/
    - some best practices
  Checkstyle is very configurable. Be sure to read the documentation at
  https://checkstyle.org (or in your downloaded distribution).
  Most Checks are configurable, be sure to consult the documentation.
  To completely disable a check, just comment it out or delete it from the file.
  To suppress certain violations please review suppression filters.
  Finally, it is worth reading the documentation.
-->

<module name="Checker">
    <!--
        If you set the basedir property below, then all reported file
        names will be relative to the specified directory. See
        https://checkstyle.org/config.html#Checker
        <property name="basedir" value="${basedir}"/>
    -->
    <property name="severity" value="error"/>

    <property name="fileExtensions" value="java, properties, xml"/>

    <!-- Excludes all 'module-info.java' files              -->
    <!-- See https://checkstyle.org/config_filefilters.html -->
    <module name="BeforeExecutionExclusionFileFilter">
        <property name="fileNamePattern" value="module\-info\.java$"/>
    </module>

    <!-- https://checkstyle.org/config_filters.html#SuppressionFilter -->
    <module name="SuppressionFilter">
        <property name="file" value="${org.checkstyle.sun.suppressionfilter.config}"
                  default="checkstyle-suppressions.xml" />
        <property name="optional" value="true"/>
    </module>

    <!-- Checks that a package-info.java file exists for each package.     -->
    <!-- See https://checkstyle.org/config_javadoc.html#JavadocPackage -->
    <module name="JavadocPackage"/>

    <!-- Checks whether files end with a new line.                        -->
    <!-- See https://checkstyle.org/config_misc.html#NewlineAtEndOfFile -->
    <module name="NewlineAtEndOfFile"/>

    <!-- Checks that property files contain the same keys.         -->
    <!-- See https://checkstyle.org/config_misc.html#Translation -->
    <module name="Translation"/>

    <!-- Checks for Size Violations.                    -->
    <!-- See https://checkstyle.org/config_sizes.html -->
    <module name="FileLength"/>
    <module name="LineLength">
        <property name="fileExtensions" value="java"/>
    </module>

    <!-- Checks for whitespace                               -->
    <!-- See https://checkstyle.org/config_whitespace.html -->
    <module name="FileTabCharacter"/>

    <!-- Miscellaneous other checks.                   -->
    <!-- See https://checkstyle.org/config_misc.html -->
    <module name="RegexpSingleline">
        <property name="format" value="\s+$"/>
        <property name="minimum" value="0"/>
        <property name="maximum" value="0"/>
        <property name="message" value="Line has trailing spaces."/>
    </module>

    <!-- Checks for Headers                                -->
    <!-- See https://checkstyle.org/config_header.html   -->
    <!-- <module name="Header"> -->
    <!--   <property name="headerFile" value="${checkstyle.header.file}"/> -->
    <!--   <property name="fileExtensions" value="java"/> -->
    <!-- </module> -->

    <module name="TreeWalker">

        <!-- Checks for Javadoc comments.                     -->
        <!-- See https://checkstyle.org/config_javadoc.html -->
        <module name="InvalidJavadocPosition"/>
        <module name="JavadocMethod"/>
        <module name="JavadocType"/>
        <module name="JavadocVariable"/>
        <module name="JavadocStyle"/>
        <module name="MissingJavadocMethod"/>

        <!-- Checks for Naming Conventions.                  -->
        <!-- See https://checkstyle.org/config_naming.html -->
        <module name="ConstantName"/>
        <module name="LocalFinalVariableName"/>
        <module name="LocalVariableName"/>
        <module name="MemberName"/>
        <module name="MethodName"/>
        <module name="PackageName"/>
        <module name="ParameterName"/>
        <module name="StaticVariableName"/>
        <module name="TypeName"/>

        <!-- Checks for imports                              -->
        <!-- See https://checkstyle.org/config_imports.html -->
        <module name="AvoidStarImport"/>
        <module name="IllegalImport"/> <!-- defaults to sun.* packages -->
        <module name="RedundantImport"/>
        <module name="UnusedImports">
            <property name="processJavadoc" value="false"/>
        </module>

        <!-- Checks for Size Violations.                    -->
        <!-- See https://checkstyle.org/config_sizes.html -->
        <module name="MethodLength"/>
        <module name="ParameterNumber"/>

        <!-- Checks for whitespace                               -->
        <!-- See https://checkstyle.org/config_whitespace.html -->
        <module name="EmptyForIteratorPad"/>
        <module name="GenericWhitespace"/>
        <module name="MethodParamPad"/>
        <module name="NoWhitespaceAfter"/>
        <module name="NoWhitespaceBefore"/>
        <module name="OperatorWrap"/>
        <module name="ParenPad"/>
        <module name="TypecastParenPad"/>
        <module name="WhitespaceAfter"/>
        <module name="WhitespaceAround"/>

        <!-- Modifier Checks                                    -->
        <!-- See https://checkstyle.org/config_modifiers.html -->
        <module name="ModifierOrder"/>
        <module name="RedundantModifier"/>

        <!-- Checks for blocks. You know, those {}'s         -->
        <!-- See https://checkstyle.org/config_blocks.html -->
        <module name="AvoidNestedBlocks"/>
        <module name="EmptyBlock"/>
        <module name="LeftCurly"/>
        <module name="NeedBraces"/>
        <module name="RightCurly"/>

        <!-- Checks for common coding problems               -->
        <!-- See https://checkstyle.org/config_coding.html -->
        <module name="EmptyStatement"/>
        <module name="EqualsHashCode"/>
        <module name="HiddenField"/>
        <module name="IllegalInstantiation"/>
        <module name="InnerAssignment"/>
        <module name="MagicNumber"/>
        <module name="MissingSwitchDefault"/>
        <module name="MultipleVariableDeclarations"/>
        <module name="SimplifyBooleanExpression"/>
        <module name="SimplifyBooleanReturn"/>

        <!-- Checks for class design                         -->
        <!-- See https://checkstyle.org/config_design.html -->
        <module name="DesignForExtension"/>
        <module name="FinalClass"/>
        <module name="HideUtilityClassConstructor"/>
        <module name="InterfaceIsType"/>
        <module name="VisibilityModifier"/>

        <!-- Miscellaneous other checks.                   -->
        <!-- See https://checkstyle.org/config_misc.html -->
        <module name="ArrayTypeStyle"/>
        <module name="FinalParameters"/>
        <module name="TodoComment"/>
        <module name="UpperEll"/>

        <!-- https://checkstyle.org/config_filters.html#SuppressionXpathFilter -->
        <module name="SuppressionXpathFilter">
            <property name="file" value="${org.checkstyle.sun.suppressionxpathfilter.config}"
                      default="checkstyle-xpath-suppressions.xml" />
            <property name="optional" value="true"/>
        </module>

    </module>

</module>
```

Это стиль разработки компании [Sun -> Oracle](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html). Затем нам необходимо сконфигурировать `Checkstyle` в системе сборке `Gradle`. Для этого необходимо отредактировать файл **build.gradle**.

Добавить плагин `checkstyle` в секцию с [плагинами](https://docs.gradle.org/current/userguide/checkstyle_plugin.html)

```groovy
plugins {
    id 'java'
    id 'io.quarkus'
    id 'jacoco'
    id 'checkstyle'
    id "org.sonarqube" version "3.3"
}
```

и добавить в конец файла следующие строки:

```groovy
checkstyle {
    toolVersion '8.44'
    configFile file("config/checkstyle/checkstyle.xml")
}

checkstyleMain {
    source ='src/main/java'
}

checkstyleTest {
    source ='src/test/java'
}

tasks.withType(Checkstyle) {
    reports {
        xml.enabled false
        html.enabled true
    }
}
```

Далее в консоли выполните команду `./gradlew checkstyleMain`. В ходе выполнения команды, выполняется анализ проекта заданный кодстайл. Как результат анализа будет сгенрирован HTML отчет

> Checkstyle rule violations were found. See the report at: file:///private/tmp/integrated-twitter/build/reports/checkstyle/main.html

В данном файле описаны все основные ошибки. 

## Задание

- проделайте все операции для настройки `checkstyle` на тестовом проекте
- настройте в [Intellij Idea поддержку](https://plugins.jetbrains.com/plugin/1065-checkstyle-idea) `checkstyle` и [настройте](https://www.jetbrains.com/help/idea/configuring-code-style.html#editorconfig) `Code Style` для Java по конфигурационному файлу
- исправьте все ошибки которые есть согласно стилю
- опишите каждое правило в файле `checkstyle.xml`
- сделайте краткое описание о инструменте `checkstyle`  

