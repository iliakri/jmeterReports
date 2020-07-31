# jmeterReports
# Описание репозитория
Данный репозиторий содержит в себе темплейт для ApacheJmeter, который поволяет генерировать и заливать отчет в Confluence. К темплейту прилагается нужное окружение для ApacheJmeter, в которое входит папка lib из корня - в ней содержатся все используемые плагины. Там же расположен chromedriver.exe, необходимый для работы темплейта. Репозиторий, помимо этого, включает в себя все необходимые для рендера графиков и анализа результатов дашборды Grafana, которые полностью интегрированы с данным темплейтом. 
# Требования
1. ApacheJmeter 5.3
2. InfluxDB 1.8
3. Grafana 7.0.0
# Grafana
На выходе вы получите несколько Grafana дашбордов:
**1. Test Trends**

<img src="https://user-images.githubusercontent.com/9977326/89025122-f32d2580-d32e-11ea-88d4-de8cc93ce4ba.png" width="90%"></img> 

Дашборд позволяет переключаться между проектами и смотреть суммарные метрики по каждому из них.

* Левая верхняя таблица - показывает тренд изменений среднего времени отклика и процента ошибок в длительных тестах (Stability). 
* Правая верхняя - аналогична левой, но показывает результаты для коротких тестов (Stress).
* Нижняя левая - содержит лог запусков по этому проекту (показывает только запуски длительность, которых превышает 3 часа - значение настраиваемое). Также имеются ссылки на подробные метрики выбранного запуска. При нажатии на ссылку попадаем в дашборд №2 - [Test Metrics](#metrics).
* Нижняя правая - содержит все запуски по всем проектам с фильтром аналогично левой таблице.

<a name="metrics"/
>**2. Test Metrics**
AAAAA
