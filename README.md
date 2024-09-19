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

<img width="627" alt="pom" src="https://github.com/user-attachments/assets/83321e08-9751-4e31-bcdc-9ee322878cf0">

<img width="1268" alt="Build after change pom" src="https://github.com/user-attachments/assets/322e2844-cff8-4ada-9bc9-95b342af22c2">

7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

<img width="900" alt="Status build" src="https://github.com/user-attachments/assets/91359619-d4a4-413a-b2c9-2fddeadcb4e0">

<img width="679" alt="Maven plaindoll" src="https://github.com/user-attachments/assets/ed1295a3-904c-4b68-a23a-e32c0e0e0975">


<img width="317" alt="Maven plaindoll2" src="https://github.com/user-attachments/assets/127cb3ea-d2b2-44b8-8edd-f538e8ebc1bc">

8. Мигрируйте `build configuration` в репозиторий.

<img width="920" alt="Migration build conf" src="https://github.com/user-attachments/assets/58a14332-f431-4455-a898-bbe46581a006">

[Link](https://github.com/sash3939/example-teamcity/tree/master/.teamcity/Netology)

9. Создайте отдельную ветку `feature/add_reply` в репозитории.

<img width="437" alt="Branch" src="https://github.com/user-attachments/assets/5c909df0-d514-498a-b598-43ce9ee88884">

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.

<img width="478" alt="New method Hunter" src="https://github.com/user-attachments/assets/7011b7f0-ab7a-4bba-b25c-d8ddf8c0dcbc">

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

<img width="534" alt="ReplicaHunter" src="https://github.com/user-attachments/assets/24969977-1f45-4e88-939e-e3974e699abb">

12. Сделайте push всех изменений в новую ветку репозитория.

<img width="752" alt="Push in new branch" src="https://github.com/user-attachments/assets/b96e2d90-affe-45b4-9c75-b526a411af5e">

[New branch](https://github.com/sash3939/example-teamcity/tree/feature/add_reply)

13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

<img width="1217" alt="Build_done_after_push" src="https://github.com/user-attachments/assets/ec13048e-288e-41fc-ad8b-9256c220ba0c">

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.

<img width="402" alt="Git merge" src="https://github.com/user-attachments/assets/b3208217-0a42-4a23-a5f7-a46e13e8fd80">

<img width="396" alt="Git merge1" src="https://github.com/user-attachments/assets/92aba8db-d9f8-4e10-aa96-f68838f1a2b9">

<img width="721" alt="Push master" src="https://github.com/user-attachments/assets/133222fd-f948-432c-b8c7-aacb7d6460a7">

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.

<img width="1041" alt="Build master after pushed" src="https://github.com/user-attachments/assets/fad3706f-5b85-4d74-83f1-1e8b0d750590">

<img width="613" alt="Artefact nexus after pushed master" src="https://github.com/user-attachments/assets/7311a773-ef88-483e-8f93-23a3468fc405">

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.

<img width="853" alt="Jar" src="https://github.com/user-attachments/assets/d3b01c1b-59d5-4b94-86a3-90b366761b42">

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

<img width="592" alt="Build after change jar in settings teamcity" src="https://github.com/user-attachments/assets/d3afac40-7313-4174-b999-dc41de0e828d">

<img width="563" alt="Nexus change after last build" src="https://github.com/user-attachments/assets/dd553eab-4384-4954-b070-2125e2dcdb52">

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.

<img width="839" alt="All settings in Repo" src="https://github.com/user-attachments/assets/e39076ef-ec27-4d11-886b-59f0ffc5f0f5">

19. В ответе пришлите ссылку на репозиторий.

[Repo_Link](https://github.com/sash3939/example-teamcity/)

---
