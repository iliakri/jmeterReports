# Описание репозитория
Данный репозиторий содержит в себе темплейт для ApacheJmeter, который поволяет генерировать и заливать отчет в Confluence. К темплейту прилагается нужное окружение для ApacheJmeter, в которое входит папка lib из корня - в ней содержатся все используемые плагины. Там же расположен chromedriver.exe, необходимый для работы темплейта. Репозиторий, помимо этого, включает в себя все необходимые для рендера графиков и анализа результатов дашборды Grafana, которые полностью интегрированы с данным темплейтом. 
## Требования к среде использования
1. ApacheJmeter 5.3
2. InfluxDB 1.8
3. Grafana 7.0.0
4. Установленный Google Chrome на машине, где будет генерироваться отчет
5. Confluence (не Cloud версия)
## Grafana
На выходе вы получите несколько Grafana дашбордов:

**1. Test Trends**

<img src="https://user-images.githubusercontent.com/9977326/89025122-f32d2580-d32e-11ea-88d4-de8cc93ce4ba.png" width="100%"></img> 

Дашборд позволяет переключаться между проектами и смотреть суммарные метрики по каждому из них.

* Левая верхняя таблица - показывает тренд изменений среднего времени отклика и процента ошибок в длительных тестах (Stability). 
* Правая верхняя - аналогична левой, но показывает результаты для коротких тестов (Stress).
* Нижняя левая - содержит лог запусков по этому проекту (показывает только запуски длительность, которых превышает 3 часа - значение настраиваемое). Также имеются ссылки на подробные метрики выбранного запуска. При нажатии на ссылку попадаем в дашборд №2 - [Test Metrics](#metrics).
* Нижняя правая - содержит все запуски по всем проектам с фильтром аналогично левой таблице.

<a name="metrics"/>**2. Test Metrics**

<img src="https://user-images.githubusercontent.com/9977326/89027755-c6c7d800-d333-11ea-97b4-3cec54facd4c.png" width="100%"></img> 
<img src="https://user-images.githubusercontent.com/9977326/89029561-68045d80-d337-11ea-8120-4d95a5427635.PNG" width="100%"></img> 
<img src="https://user-images.githubusercontent.com/9977326/89029704-aa2d9f00-d337-11ea-95c3-7f9e222786b8.PNG" width="100%"></img>
<img src="https://user-images.githubusercontent.com/9977326/89030566-676cc680-d339-11ea-904f-0d97978a48d1.png" width="100%"></img>
<img src="https://user-images.githubusercontent.com/9977326/89030707-b155ac80-d339-11ea-9e2f-832b9b9e22b4.PNG" width="100%"></img>


На этом дашборде собрана полная информация по выбранному тесту. Вручную можно выбрать:
* Проект
* Количество отображаемых запусков
* Нужный запуск
* Конкретную операцию этого запуска. По ней повятся детальные метрики в конце дашборда
Этот дашборд используется для осмотра результатов и их анализа.

**3. Render Dash**

Данный дашборд аналогичен дашборду №2 - [Test Metrics](#metrics), но он содержит определенные фильтры и настройки, которые снижают наглядность результатов, но необходимы для рендеринга. К примеру, на нем отключена пагинация в таблицах и графики содержат топ 5 операций, остальные вынесены в "Other".

# Jmeter

В самом ApacheJMeter для использования темплейта, после его [установки](#install), достаточно просто нажать на вкладку File, выбрать Templates..., кликнуть в выпадающем списке на "Add autogenerated reports..." и нажать на Merge
<img src="https://user-images.githubusercontent.com/9977326/89032614-b583c900-d33d-11ea-8b84-b8d00d7fb20a.png" width="100%"></img>
После добавления получится такой тест-план:

<img src="https://user-images.githubusercontent.com/9977326/89034199-2a0c3700-d341-11ea-83dd-ca827f22dacf.png" width="45%" align="left"></img>

<br>

* Тут объявляем все необходимые нам переменные
<br>

* Этот служебный запрос создает в базе метку начала теста, находится в SetUp Thread Group, а значит - выполняется до теста
* Вместо этой Thread Group размещается любой ваш скрипт
* Главное, в случае если Thread Groups несколько, каждая содержала эти Listeners, они отправляют запросы и ошибки в influxDB
* Эти Listners необходимо выносить за пределы всех Thead Groups, View Results Tree - отладка, Simpe Data Writer - создает файл результатов для просмотра голых данных
аААааф

ААаАф

АА
