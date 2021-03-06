# Задание к занятию "XML и JSON"

## Стандартная сериализация объектов ИБ

### Описание задачи

Записать в файл XML объект справочника и прочитать его в другой информационной базе.
Повторить операцию, но использовать для обмена формат JSON.

### Требования к результату

Внешняя обработка, позволяющая выбрать элемент справочника и сохранить (сериализовать) его в файл данных. Эта же обработка должна позволять выбрать файл на диске и создать на основании его содержимго элемент справочника (десериализовать). Внешняя обработка должна обеспечивать обмен записями справочника между несколькими информационными базами идентичной структуры.

### Процесс выполнения

1. Возьмите чистую конфигурацию и создайте в ней справочник "Товары". Создайте реквизиты справочника "Цена (Число 18.2)", "Артикул (Строка 15)", "Брэнд Строка (50)"
2. Создайте внешнюю обработку с двумя закладками "Запись в файл" и "Чтение из файла"
3. На закладке "Запись в файл" разместите поле выбора "Товар" для выбора элемента из справочника Товары, а также кнопку "Сохранить в файл"
4. В обработчике нажатия кнопки "Сохранить в файл" вызовите диалог выбора файла с фильтром по расширению XML
5. Добавьте в модуль формы метод "Сохранение" с одним параметром - `ВыбранныйПуть`
6. После выбора файла пользователем должен быть вызван метод "Сохранение" с передачей в него параметром выбранного пользователем имени файла
7. Реализуйте метод "Сохранение" с использованием объекта ЗаписьXML. В файл должен быть записан СправочникОбъект той записи, которая выбрана в поле "Товар". Обратите внимание, в файл должна быть записана не ссылка, а именно СправочникОбъект, т.е. необходимо вызвать метод ПолучитьОбъект у ссылки в поле "Товар"
8. Для записи объекта используйте метод глобального контекста `ЗаписатьXML`. Изучите содержимое полученного файла.
9. На закладке "Чтение из файла" разместите кнопку "Прочитать файл"
10. В обработчике нажатия кнопки откройте диалог выбора файла и дайте пользователю возможность выбрать XML файл для загрузки
11. После выбора файла напишите алгоритм чтение файла с помощью объекта ЧтениеXML
12. Для чтения из файла в СправочникОбъект используйте метод глобального контекста `ПрочитатьXML`. Не забудьте вторым параметром метода указать тип, в который нужно прочитать (десериализовать) объект справочника.

В результате, должна получиться внешняя обработка, которая позволит передать запись справочника "Товары" между двумя одинаковыми информационными базами через файл XML.

13. Скопируйте получившуюся обработку и модифицируйте ее таким образом, чтобы вместо объектов ЧтениеXML и ЗаписьXML использовались объекты ЧтениеJSON и ЗаписьJSON соответственно.

# Задание "Ручное формирование XML"

## Описание задачи

Довольно часто требуется не просто записать данные базы в XML-файл, а соблюсти определенную структуру файла, имена полей и их формат. Для этих целей используется ручное поэлементное формирование документа XML.

### Требования к результату

Внешняя обработка, создающая документ передачи данных о бронировании в гипотетический отель.
Результат записи XML обработка должна выводить в поле текстового документа, расположенное на форме этой обработки.

### Процесс выполнения 

1. Создайте внешнюю обработку с кнопкой, нажатие на которую формирует файл следующего содержания, используя методы объекта `ЗаписьXML`

```xml
<?xml version="1.0" encoding="utf-8"?>
<guests>
    <guest name="Иван" arrives="2020-08-25">
      <room>
         <type>double</type>
         <withShower>true</withShower>
      </room>
      <meals breakfast="true" dinner="false" supper="false" />
    </guest>
    <guest name="Петр" arrives="2020-09-10">
      <room>
         <type>single</type>
         <withShower>true</withShower>
      </room>
      <meals breakfast="true" dinner="true" supper="true" />
    </guest>
</guests>
```

Вам потребуются методы:

* ЗаписатьОбъявлениеXML
* ЗаписатьНачалоЭлемента
* ЗаписатьКонецЭлемента
* ЗаписатьАтрибут
* ЗаписатьТекст

2. Выведите XML в виде строки в поле текстового документа, размещенное на форме обработки.

# Задача "Формирование JSON"

## Описание задачи

Формат JSON является более легковесным, и на практике чаще всего является текстовым представлением того или иного объекта (например, Структуры)
Ручное формирование JSON поэлементно используется редко, поэтому в данном задании будет применена методика создания JSON из готового объекта, как наиболее частая.

## Требования к результату

Внешняя обработка, выводящая в поле текстового документа содержимое коллекции для передачи в гипотетический отель для бронирования

Результат должен иметь вид:

```json
[
  {
    "name": "Иван",
    "arrives": "2020-08-25",
    "room": {
      "type": "double",
      "withShower": true
    },
    "meals": [
      "brealfast"
    ]
  },
  {
    "name": "Петр",
    "arrives": "2020-09-10",
    "room": {
      "type": "single",
      "withShower": true
    },
    "meals": [
      "brealfast",
      "dinner",
      "supper"
    ]
  }
]
```

Обратите внимание, что в JSON существуют Структуры (Объекты) обозначенные фигурными скобками, и Массивы, обозначенные квадратными скобками. Каждый тип 1С:Предприятия при записи в JSON отображается именно в эти элементы JSON. Иными словами, для списков в квадратных скобках применяются Массивы 1С, для объектов в фигурных скобках - Структуры 1С или Соответствия.

## Процесс выполнения

1. Разместите на форме внешней ообработки поле текстового документа и кнопку "Создать JSON"
2. В обработчике нажатия кнопки создайте структуру для "Гостя", в качестве имен свойств структуры используйте именно такие названия, как в требуемом примере документа "name, arrives" и т.д. Для "комнат" и "питания" также используйте коллекции 1С.
3. Создайте Массив таких "гостей", как в примере (2 записи-структуры) в Массиве
4. С помощью метода глобального контекста `ЗаписатьJSON` и объекта `ЗаписьJSON` запишите массив гостей в виде JSON
5. Результат записи, в виде строки, отобразите в поле текстового документа на форме обработки.