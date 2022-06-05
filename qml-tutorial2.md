
# QML Самоучитель
## Глава 2 - Компоненты QML

В этой главе описывается средство для изменения цвета текста.

![](https://github.com/SlimRG/QML-Tutorial/blob/main/declarative-tutorial2.png)

На скриншоте выше изображен набор цветов, состоящий из шести ячеек с разными цветами. Чтобы избежать повторения одного и того же кода для каждой ячейки, создается новый компонент ячейки (компонент *Cell*). Компонент предоставляет способ определения нового типа, который можно повторно использовать в других файлах QML. Компонент QML подобен черному ящику и взаимодействует с внешним миром через свойства, сигналы и функции и обычно определяется в его собственном файле QML. (см. [Документацию по Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)). Имя файла компонента всегда должно начинаться с заглавной буквы английского алфавита.

Ниже показан QML код для *Cell.qml*:
```QML
import  QtQuick 2.0
  
Item {
   id: container
   property alias cellColor: rectangle.color
   signal clicked(cellColor: color)

   width: 40; height: 25

   Rectangle {
      id: rectangle
      border.color: "white"
      anchors.fill: parent
   }

   MouseArea {
      anchors.fill: parent
      onClicked: container.clicked(container.cellColor)
   }
}
```
### Разбор по шагам
#### Cell компонент
```QML
Item {
   id: container
   property alias cellColor: rectangle.color
   signal clicked(cellColor: color)

   width: 40; height: 25
```

Корневой тип нашего компонента - это элемент ([Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)) с идентификатором (*ID*) равным *container*. Элемент (*Item*) является самым основным визуальным типом в QML и часто используется в качестве контейнера для других типов.

```QML
property  alias  cellColor:  rectangle.color
```
Выше объявляется свойство *cellColor* (цвет ячейки). Данное свойство доступно извне компонента, это позволяет создавать экземпляры ячеек с разными цветами. Это свойство является просто псевдонимом существующего свойства - цвета прямоугольника, составляющего ячейку (см. [Привязку свойства](https://doc.qt.io/qt-6/qtqml-syntax-propertybinding.html)).

```QML
signal clicked(cellColor: color)
```
Также нужно, чтобы у нашего компонента был сигнал, который мы вызываем при нажатии (*clicked*) с параметром цвета ячейки типа цвета (*color*). Позже мы будем использовать данный сигнал для изменения цвета текста в основном файле QML.

```QML
Rectangle {
   id: rectangle
   border.color: "white"
   anchors.fill: parent
}
```
Компонент ячейки в основном представляет собой цветной прямоугольник с идентификатором (*ID*) *rectangle*.

Свойство *anchors.fill* - это удобный способ задать размер визуального типа. В этом случае прямоугольник будет иметь тот же размер, что и его родительский (parent) элемент (см. [Макет на основе привязки](https://doc.qt.io/qt-6/qtquick-positioning-anchors.html)).

```QML
MouseArea {
   anchors.fill: parent
   onClicked: container.clicked(container.cellColor)
}
```

Чтобы изменить цвет текста при щелчке по ячейке, создается тип [MouseArea](https://doc.qt.io/qt-6/qml-qtquick-mousearea.html) (область мышки) с тем же размером, что и ее родительский элемент.

#### Основной файл QML
В основном файле QML используется ранее созданный компонент Cell для создания средства выбора цвета:

```QML
import QtQuick 2.0

Rectangle {
   id: page
   width: 320; height: 480
   color: "lightgray"
   
   Text {
      id: helloText
      text: "Hello world!"  
      y: 30
      anchors.horizontalCenter: page.horizontalCenter
      font.pointSize: 24; font.bold: true
   }

   Grid {
      id: colorPicker
      x: 4; anchors.bottom: page.bottom; anchors.bottomMargin: 4
      rows: 2; columns: 3; spacing: 3

      Cell { cellColor: "red"; onClicked: helloText.color = cellColor }
      Cell { cellColor: "green"; onClicked: helloText.color = cellColor }
      Cell { cellColor: "blue"; onClicked: helloText.color = cellColor }
      Cell { cellColor: "yellow"; onClicked: helloText.color = cellColor }
      Cell { cellColor: "steelblue"; onClicked: helloText.color = cellColor }
      Cell { cellColor: "black"; onClicked: helloText.color = cellColor }
      }
}
```

Создается средство выбора цвета, представляя собой сетку из 6 ячеек с разными цветами.

Когда срабатывает сигнал щелчка мыши (*clicked signal*) по ячейке, установится цвет текста равным цвету ячейки, переданному в качестве параметра *cellColor*.  Можно реагировать на любой сигнал нашему компоненту с помощью свойства с именем *'onSignalName'* (см. [Атрибуты сигнала](https://doc.qt.io/qt-6/qtqml-syntax-objectattributes.html#signal-attributes)).

<-- [Базовые Типы](https://github.com/SlimRG/QML-Tutorial/blob/main/qml-tutorial1.md "Базовые Типы")  

[Состояния и переходы](https://github.com/SlimRG/QML-Tutorial/blob/main/qml-tutorial3.md "Состояния и переходы") -->

<hr/>
© 2022 The Qt Company Ltd. Documentation contributions included herein are the copyrights of their respective owners. The documentation provided herein is licensed under the terms of the GNU Free Documentation License version 1.3 (https://www.gnu.org/licenses/fdl.html) as published by the Free Software Foundation. Qt and respective logos are trademarks of The Qt Company Ltd. in Finland and/or other countries worldwide. All other trademarks are property of their respective owners.

