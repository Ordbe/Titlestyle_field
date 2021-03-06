### Описание задачи
> На рисунках ниже представлен конфигурационный файл виджета «Текст». Требуется коротко описать как покрыть функционал блока «titleStyle» в достаточном объеме и, при этом, минимизировать количество проверок. ![Конфигурационный файл виджета "Текст"](https://github.com/Ordbe/Titlestyle_field/blob/main/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F%20%D0%BF%D0%BE%D0%BB%D1%8F%20%D1%82%D0%B5%D0%BA%D1%81%D1%82.png)

### Описание проверок
1. для начала следует проверить тот сценарий, где никакие параметры не указываются и выставляются по дефолту.
2. для минимального количества остальных тест-кейсов следует выделить атомарные изменения виджета (например, изменение цвета на RED без изменения остальных параметров). 

### Сокращение количества проверок  
  Атомарные сценарии можно покрыть тестами с помощью матрицы трассировки, но такой подход увеличит количество тест-кейсов до полного количества параметров из требований. Чтобы снизить количество тестов следует попарно протестировать все атомарные изменения. При этом вероятность возникновения бага при снижении количества тестов попарным тестированием возрастет несущественно. 
  При попарном тестировании возникают особенные условия параметров vertical и rotate, что тоже нужно учесть. Для обозначения сценариев я бы использовал [pairwise generator](https://pairwise.teremokgames.com/) во избежание ошибок при самостоятельном составлении. Для составления сценариев указал бы значения всех параметров, а также условия:
- "vertical=true" can only exists with "position=left" 
- "vertical=true" can only exists with "position=right"
- "rotate=true" can only exists with "vertical=true". 
	
Дополнительно следует учесть возможность использования titlestyle в различных виджетах. Для этого возможно три варианта включения виджетов в общий список проверок:
- добавление виджетов в качестве параметров при попарном тестировании
- тестирование всех сценариев для каждого виджета
- выборочное прохождение нескольких сценариев попарного тестирования в пайплайне регрессионного тестирования

