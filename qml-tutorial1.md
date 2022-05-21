# QML Самоучитель
## Глава 1 - Базовые Типы

Первая программа представляет собой очень простой "Hello world" пример, который познакомит вас с некоторыми базовыми концепциями QML.

На рисунке ниже показан скриншот этой программы:

![](https://github.com/SlimRG/QML-Tutorial/blob/main/declarative-tutorial1.png)

QML код приложения:
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
}
```

### Разбор по шагам
#### Импорт
Сперва нужно импортировать типы, которые нужны вам для этого примера. Большинство файлов QML импортируют встроенные типы QML (например, [Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html "Rectangle"), [Image](https://doc.qt.io/qt-6/qml-qtquick-image.html "Image"), ...), которые поставляются с Qt, используя:
```QML
import QtQuick 2.0
```

#### Тип - Прямоугольник
```QML
Rectangle {
    id: page
    width: 320; height: 480
    color: "lightgray"
```

Здесь объявляется корневой объект типа [Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html "Rectangle") (Прямоугольник). Это один из основных строительных блоков, которые вы можете использовать для создания приложения на QML. Далее ему присваивается идентификатор, чтобы была возможность ссылаться на него в дальнейшем. В данном случае идентификатор имеет значение "page". Также устанавливаются свойства ширины, высоты и цвета. Тип [Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html "Rectangle") содержит много других свойств (таких как *x* и *y*), но они будут инициированы со значениями по умолчанию.

#### Тип - Текст
```QML
Text {
    id: helloText
    text: "Hello world!"
    y: 30
    anchors.horizontalCenter: page.horizontalCenter
    font.pointSize: 24; font.bold: true
}
```

Здесь добавляется тип [Text](https://doc.qt.io/qt-6/qml-qtquick-text.html "Text") в качестве дочернего элемента корневого типа Rectangle, который отображает текст "Hello world!".

Свойство *y* используется для позиционирования текста по вертикали на расстоянии 30 пикселей от верхней части его родительского элемента.

Свойство *anchors.horizontalCenter* прикладывается к горизонтальному центру типа. В этом случае указывается, что тип Text должен быть горизонтально центрирован в элементе "page" (см. [Anchor-Based Layout](https://doc.qt.io/qt-6/qtquick-positioning-anchors.html "Anchor-Based Layout")).

Размер *font.pointSize* и *font.bold* связаны со шрифтами и используют точечную нотацию.

### Просмотр примера
Чтобы просмотреть то, что вы создали, запустите инструмент qml (расположенный в каталоге bin) с вашим именем файла в качестве первого аргумента. Например, чтобы запустить предоставленный пример завершенной Главы 1 из места установки, вы должны ввести:

```shell
qml tutorials/helloworld/tutorial1.qml
```

<-- [Главная страница](https://github.com/SlimRG/QML-Tutorial/blob/main/qml-tutorial.md "Главная страница")  

[Компоненты QML](https://github.com/SlimRG/QML-Tutorial/blob/main/ "Глава 2 - Компоненты QML") -->

<hr/>
© 2022 The Qt Company Ltd. Documentation contributions included herein are the copyrights of their respective owners. The documentation provided herein is licensed under the terms of the GNU Free Documentation License version 1.3 (https://www.gnu.org/licenses/fdl.html) as published by the Free Software Foundation. Qt and respective logos are trademarks of The Qt Company Ltd. in Finland and/or other countries worldwide. All other trademarks are property of their respective owners.

