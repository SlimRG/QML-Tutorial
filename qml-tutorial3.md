
# QML Самоучитель
## Глава 3 - Состояния и переходы

В данной главе предыдущий пример станет немного более динамичным, используя состояния и переходы.

Нужно, чтобы текст перемещался в нижнюю часть экрана, поворачивался и становился красным при нажатии.

![](https://github.com/SlimRG/QML-Tutorial/blob/main/ezgif-3-4d6fe02895.gif)

Ниже приведен QML код:
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

      MouseArea { id: mouseArea; anchors.fill: parent }

      states: State {
         name: "down"; when: mouseArea.pressed == true
         PropertyChanges {
            helloText {
               y: 160
               rotation: 180
               color: "red"
            }
        }
      }  

      transitions: Transition {
         from: ""; to: "down"; reversible: true
         ParallelAnimation {
            NumberAnimation { properties: "y,rotation"; duration: 500; easing.type: Easing.InOutQuad }
            ColorAnimation { duration: 500 }
         }
      }
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

### Разбор по шагам
#### Cell компонент

```QML
states: State {
   name: "down"; when: mouseArea.pressed == true
   PropertyChanges {
      helloText {
         y: 160
         rotation: 180
         color: "red"
      }
   }
}
```
Сначала создается новое состояние *down* для текстового типа. Это состояние будет активироваться при нажатии кнопки мышки и деактивироваться при ее отпускании.

Состояние *down* включает в себя набор изменений свойств из неявного дефолтного (default) состояния (элементы в том виде, в каком они были изначально определены в QML). В ручную (специально) устанавливаются свойства текста равными: положение по вертикали (*y*) равное 160, поворот - 180 и цвет - красный.

```QML
transitions: Transition {
   from: ""; to: "down"; reversible: true
   ParallelAnimation {
      NumberAnimation { properties: "y,rotation"; duration: 500; easing.type: Easing.InOutQuad }
      ColorAnimation { duration: 500 }
  }
}
```
Чтобы текст появлялся внизу не мгновенно, а перемещался плавно - добавляется переход между нашими двумя состояниями. 

"from" и "to" определяют состояния, между которыми будет выполняться переход. В этом случае происходит переход из состояния по умолчанию в состояние *down*.

Поскольку требуется, чтобы тот же переход выполнялся в обратном порядке при возврате из состояния *down* в дефолтное состояние, мы устанавливаем значение reversable равным true. Это эквивалентно записи двух переходов по отдельности.

Тип *ParallelAnimation* гарантирует, что два типа анимации (число и цвет) запускаются одновременно (параллельно). Также возможно бы запускать их один за другим, используя вместо этого *SequentialAnimation*.

Дополнительные сведения о состояниях и переходах см. в разделе [Состояния QtQuick](https://doc.qt.io/qt-6/qtquick-statesanimations-states.html), а также [Пример реализации состояний и переходов](https://doc.qt.io/qt-6/qtquick-animation-example.html#states).

<-- [Базовые Типы](https://github.com/SlimRG/QML-Tutorial/edit/main/qml-tutorial1.md "Базовые Типы")  

[Состояния и переходы](https://github.com/SlimRG/QML-Tutorial/blob/main/ "Состояния и переходы") -->

<hr/>
© 2022 The Qt Company Ltd. Documentation contributions included herein are the copyrights of their respective owners. The documentation provided herein is licensed under the terms of the GNU Free Documentation License version 1.3 (https://www.gnu.org/licenses/fdl.html) as published by the Free Software Foundation. Qt and respective logos are trademarks of The Qt Company Ltd. in Finland and/or other countries worldwide. All other trademarks are property of their respective owners.

