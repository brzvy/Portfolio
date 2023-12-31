# A/B тестирование

# Проверка внедрения улучшенной рекомендательной системы.

## Цель исследования:

- Оценить корректность проведения теста и проанализировать его результаты.
   
  - удостовериться, что нет пересечений с конкурирующим тестом и нет пользователей, участвующих в двух группах теста одновременно;

  - проверить равномерность распределения пользователей по тестовым группам и правильность их формирования.

## Техническое задание:

- Название теста: recommender_system_test;

- группы: А — контрольная, B — новая платёжная воронка;

- дата запуска: 2020-12-07;

- дата остановки набора новых пользователей: 2020-12-21;

- дата остановки: 2021-01-04;

- аудитория: в тест должно быть отобрано 15% новых пользователей из региона EU;

- назначение теста: тестирование изменений, связанных с внедрением улучшенной рекомендательной системы;

- ожидаемое количество участников теста: 6000;

- ожидаемый эффект: за 14 дней с момента регистрации пользователи покажут улучшение каждой метрики не менее, чем на 10%:
                   
                   - конверсии в просмотр карточек товаров — событие product_page ,
                   - просмотры корзины — product_cart ,
                   - покупки — purchase.

## Вывод:

В ходе работы было сделана:

- **Предобработка:**
   - По четырем таблицам были просмотрены:
      - Дубликаты
        - Дубликаты не обнаружены
  
      - Пропуски
        - В таблице events были обнаружены пропуски, определена их связь и принято решение оставить данные пропуски.
        - В других таблицах не обнаружены пропуски.
  
      - Типы данных таблиц
        - В таблицах были изменены колонки с датой на дату.

- **Изучение и проверка данных:**
   - Условие ТЗ: дата остановки набора новых пользователей: 2020-12-21 **выполняется**

   - Задание ТЗ:

  дата запуска: 2020-12-07

  дата остановки: 2021-01-04

  В нашем случае дата запуска сходится с ТЗ

  Но **дата остановки теста не сходится** с последними действями участниками, которые были сделаны: 2020-12-30 в 23-36.

  Что может быть связано с праздниками, либо с перебоями в работе системы из-за праздников.

  Несхождение с ТЗ может быть опасно, так как мы не имеем полноту данных, что стоит учитывать, при дальнейшем анализе.


  - При проведении нашего теста, можно заметить, что в это врмея провоидилсь две акции:

  Christmas&New Year Promo для регионов EU, N America, но стоит заметить, что данная акция начала проводиться после того, как закрылся набор участников(что подверждено ТЗ)

  CIS New Year Gift Lottery для регионов CIS, но также старт данного мероприятия был организован после набора участников тестирования.

  Точно убедиться в том, влияют ли данные акции на участников теста, затруднительно, так как нет информации, кто участвовал в данных мероприятиях.

  - В тесте recommender_system_test пересечений между пользователями в группах нет.

  - Между нашим тестом и конкурирующим есть пересекающие пользователи и их количество равно 1602 человека. 

  - Статистически значимых различий между группами в количестве участников в нашем тесте нет(до определение лайфтайма).

  - Можно заметить примерно равное формирование групп, однако 2020-12-10 участников в группе В больше зарегитрировалось, нежели в группе А.

  Пики регистраций сходятся, так как 17, 14 и 21 являются понедельниками, следовательно пользователи более активно регистрировались по понедельникам.

  - Задание ТЗ:ожидаемый эффект: за 14 дней с момента регистрации пользователи покажут улучшение каждой метрики не менее, чем на 10%: конверсии в просмотр карточек товаров — событие product_page , просмотры корзины — product_cart , покупки — purchase.

  ТЗ **не выполняется**


**Исходя из проверки данныхЮ судить о коректности теста трудно, так как множество ТЗ не выполняется, что может менять результаты анализа, в том числе и дальнейших действий.**


- **Исселодовательский анализ:**
  - Кооличество действий на участника в выборках распределены не одинаково, видно, что в группе А более активные участники, нежели в группе В.

  - По графику можно заметить, что участники группы А со временем количество действим начинает убывать. Но в среднем количество дейстий равно около 60-70%. У группы B можно увидеть тендецию на возрастание в количестве действий по дням, однако в процентном соотношении количество действий в 2 раза меньше нежели, чем у группы А.

  Таким образом, стоит отметить различность количества действий у выборок по дням, так как она весома.

  - По воронке событий можно сделать вывод, что с регистрации на страницу продукта в группе А перешло 65% учатсников, тогда как в группе В 56, то есть меньше на 9% количество участников перешло с регистрации, что уже не входит в ТЗ.

  С страницы продукта в переход на карту продукта в группе А 47%, в группе В 51%, то есть больше на 4% учатсников, однако это так же не входит в ожидаемое ТЗ.

  На оплату в группе А перешло 96%, тогда как в группе В 94%, разница в 2%, в пользу А группы.

  Таким образом ожидаемое ТЗ не выполняется.

  Уже можно заметить, что улучшения, уменьшили для нашей группы покупки на 2%.

  - По двум тестам не удалось отвергнуть нулевую гипотезу: Различий в количестве пользователей между группами нет.
  

По вышесделанным графикам, можно сделать вывод, что:

- По распределению количества дейтсвий на участника, более активные пользователи в группе А, следовательно, улучшения не повысили данный параметр.

- По распределению количеству действий по дате, так же можно заметить,что в группе А более активные пользователи, следовательно, улучшения не повысили данный параметр.

- На оплату в группе А перешло 96%, тогда как в группе В 94%, разница в 2%, в пользу А группы. Следовательно, улучшения не повысили конверсию.

Можно сделать предворительный вывод, что А/В тест не подтвердил ожидания. Так как группа А успешнее по многим показателям.


- **z-тест:**
  - По выводу, можно увидеть, что: Для контрольной группы А и экспериментальной B и  всех событий не удалось отвергнуть нулевую гипотезу: различий в долях в количестве пользователей между группами нет. Кроме одного события: переход на страницу продукта, где по воронке, можно было заметить, что в группе А больше конверсия нежели в группе В.

  Следовательно между данными группами нет статистически значимых различий по количтесву пользователей, кроме одного параметра.
  
  
**Вывод:**
Не было выявлено различий в статистической значимости между контрольной и экспериментальной, следовательно, **внедрение улучшенной рекомендательной системы, не улучшило конверсию, скорее ухудшило.**

