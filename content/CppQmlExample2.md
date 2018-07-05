([C++](Cpp.md)) [QmlExample2](CppQmlExample2.md)
==================================================

 

Technical facts
---------------

 

[Operating system(s) or programming environment(s)](CppOs.md)

-   ![Lubuntu](PicLubuntu.png) [Lubuntu](CppLubuntu.md) 15.04 (vivid)

[IDE(s)](CppIde.md):

-   ![Qt Creator](PicQtCreator.png) [Qt Creator](CppQtCreator.md) 3.1.1

[Project type](CppQtProjectType.md):

-   ![console](PicConsole.png) [Console
    application](CppConsoleApplication.md)

[C++ standard](CppStandard.md):

-   ![C++98](PicCpp98.png) [C++98](Cpp98.md)

[Compiler(s)](CppCompiler.md):

-   [G++](CppGpp.md) 4.9.2

[Libraries](CppLibrary.md) used:

-   ![STL](PicStl.png) [STL](CppStl.md): GNU ISO C++ Library, version
    4.9.2

 

 

 

 

 

[Qt project file](CppQtProjectFile.md): ./CppQmlExample2/CppQmlExample2.pro
----------------------------------------------------------------------------

```
include(../../DesktopApplication.pri)
include(../../Libraries/GeneralConsole.pri)
include(../../Classes/CppCaesarCipher/CppCaesarCipher.pri)
include(../../Classes/CppLoopReader/CppLoopReader.pri)

TEMPLATE = app

QT += qml quick

SOURCES += main.cpp

RESOURCES += qml.qrc

# Additional import path used to resolve QML modules in Qt Creator's code model
QML_IMPORT_PATH =

# Default rules for deployment.
include(deployment.pri)
OTHER_FILES += \
    qmlcaesarcipher.qml
```
 

 

 

./CppQmlExample2/deployment.pri
-------------------------------

 
```
android-no-sdk {
    target.path = /data/user/qt
    export(target.path)
    INSTALLS += target
} else:android {
    x86 {
        target.path = /libs/x86
    } else: armeabi-v7a {
        target.path = /libs/armeabi-v7a
    } else {
        target.path = /libs/armeabi
    }
    export(target.path)
    INSTALLS += target
} else:unix {
    isEmpty(target.path) {
        qnx {
            target.path = /tmp/$${TARGET}/bin
        } else {
            target.path = /opt/$${TARGET}/bin
        }
        export(target.path)
    }
    INSTALLS += target
}

export(INSTALLS)
```
 

 

 

 

./CppQmlExample2/main.cpp
-------------------------

 

```
#include <QGuiApplication>
#include <QQmlApplicationEngine>

#include <QtQml>
#include "caesarcipher.h"

struct QmlCaesarCipher : public QObject
{
  QmlCaesarCipher(const int key = 0) : m_cipher(key) {}
  ribi::CaesarCipher m_cipher;
};

int main(int argc, char *argv[])
{
    QGuiApplication app(argc, argv);

    //qmlRegisterType<testClass>("MyCustomQMLObjects", 2, 35, "testClassNameInQML");
    qmlRegisterType<QmlCaesarCipher>("QmlCaesarCipher", 2, 35, "QmlCaesarCipher1");

    QQmlApplicationEngine engine;
    engine.load(QUrl(QStringLiteral("qrc:///main.qml")));

    return app.exec();
}
```
 

 

 

 

 

./CppQmlExample2/piechart.h
---------------------------

```
#ifndef PIECHART_H
#define PIECHART_H

#include <QObject>

class piechart : public QObject
{
    Q_OBJECT
public:
    explicit piechart(QObject *parent = 0);

signals:

public slots:

};

#endif // PIECHART_H
```

./CppQmlExample2/piechart.cpp
-----------------------------

```
#include "piechart.h"

piechart::piechart(QObject *parent) :
    QObject(parent)
{

}
```