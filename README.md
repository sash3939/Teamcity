# Домашнее задание к занятию 11 «Teamcity»

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

<img width="1166" alt="VM" src="https://github.com/user-attachments/assets/db813039-d81a-4ee9-b41d-eb06697d2f77">

<img width="720" alt="Nexus" src="https://github.com/user-attachments/assets/0021fe3f-7856-49cb-b777-3735a64db5b5">

<img width="748" alt="Teamcity" src="https://github.com/user-attachments/assets/b3206c05-7b4f-4eb8-919c-51010c1f31b8">

<img width="806" alt="Authorize agent" src="https://github.com/user-attachments/assets/b5029c3b-0a7a-44d4-804f-84a7e7d9d07f">


## Основная часть

1. Создайте новый проект в teamcity на основе fork.

<img width="726" alt="Create project" src="https://github.com/user-attachments/assets/453ce6d7-f378-4e59-8737-f80b9a21d4ed">

<img width="1234" alt="Created project" src="https://github.com/user-attachments/assets/3ea3b533-7639-43cc-af18-4527b3a9491a">

2. Сделайте autodetect конфигурации.

<img width="1169" alt="Autodetect" src="https://github.com/user-attachments/assets/a590a52b-c461-4277-bc36-478575e2809f">

3. Сохраните необходимые шаги, запустите первую сборку master.

<img width="1100" alt="Build0" src="https://github.com/user-attachments/assets/8132948d-a954-402d-850c-6641defdd52e">

<img width="1265" alt="Build" src="https://github.com/user-attachments/assets/98f7d086-4f59-49ef-b539-83a618580db0">

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.

<img width="1022" alt="Change build" src="https://github.com/user-attachments/assets/c1cfed0b-3555-4b8f-aa12-2ffab3c4446a">

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

<img width="1186" alt="settings" src="https://github.com/user-attachments/assets/e3f41b59-472a-4be1-9008-5c88f21e38bb">

<img width="718" alt="Build with settings" src="https://github.com/user-attachments/assets/bf2297fd-f215-43cc-8051-e0ef342bb5ab">


6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.
8. Мигрируйте `build configuration` в репозиторий.
9. Создайте отдельную ветку `feature/add_reply` в репозитории.
10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.
11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.
12. Сделайте push всех изменений в новую ветку репозитория.
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

---
