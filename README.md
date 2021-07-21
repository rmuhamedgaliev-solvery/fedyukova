# О проекте

Привет! Это учебный репозиторий в рамках консультаций для проекта Solvery.

# Содержание

- [Консультации](doc/meetups/README.md)


# ‼️ Цель:

- необходимы знания по повышению качества разрабатываемого продукта
- максимизировать автоматизацию для уменьшения рутины
- обучиться базовым инструментам автоматизации и повышения качества

# ⚠️ Что можно сделать:

- определить основные проблемные места, что бы подобрать требуемые инструменты
- собрать статистику по существующим проектам и собрать общий дашборд "здоровья" проектов
    - познакомится с [SonarQube](https://www.sonarqube.org)
    - синхронизировать данные в [Grafana](https://grafana.com)
- ознакомиться с различными системами CI (Jenkins/Travis, etc.)
- договориться о стиле кода при разработке
- ознакомится со статическими анализаторами
    - [checkstyle](https://checkstyle.sourceforge.io)
    - [findbugs](http://findbugs.sourceforge.net)
    - [PMD](https://pmd.github.io)
    - [jacoco](https://github.com/jacoco/jacoco)
- реализовать бота, который будет назначать ревьювера из списка настроенного для проекта
- запретить пуш в мастер всем разработчикам
- настроить проверку пуллреквеста при мерже в главную ветку и запрещать мере при отклонении одного из критерия
- настроить запуск автоматических тестов перед новым релизом
- настроить pre-commit и pre-push руки для контроля качества кода перед заливкой на удаленный сервер
- проводить ретроспективу полученых результатов