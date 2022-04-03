# qt-5.12.4-MySql-Driver
## What is the problem?
Qt 5.12.4 has removed the plugings to connect to MySql database due to licence changes which you can find it in [Qt bug reports website](https://bugreports.qt.io/browse/QTBUG-76081). <br> So you need to build the libraries on your own or downloading here.
 ### Windows
 #### Mingw x64 Binraries
For dowloading the file for Mingw x64 compiler, click [this](qt5_12_4_mysql_dlls_mingwx64.zip). Unzip the file and copy its content into `C:\Qt\Qt5.12.4\5.12.4\mingw73_64`. `libmysql.dll` goes to `bin` directory whereas `qsqlmysqld.dll` and `qsqlmysql.dll` go into `plugins\sqldrivers` directory. Note that it is assumed that Qt 5.12.4 is installed on the `C` Drive.
#### Building on your own:
For mingw x64 you can simply download the file. For other compilers I did not compile the code yet. So you need to build the library on your own.
To do this, first download `MySql Server` from [here](https://dev.mysql.com/downloads/installer/) and install it on your PC. Then go to `C:\Qt\Qt5.12.4\5.12.4\Src\qtbase\src\plugins\sqldrivers\mysql`, open `mysql.pro` file in Qt Creator and replace the content below in the file:

``` qmake
TARGET = qsqlmysql

HEADERS += $$PWD/qsql_mysql_p.h
SOURCES += $$PWD/qsql_mysql.cpp $$PWD/main.cpp

#QMAKE_USE += mysql

OTHER_FILES += mysql.json

PLUGIN_CLASS_NAME = QMYSQLDriverPlugin

win32:LIBS += -L"C:\Program Files\MySQL\MySQL Server 8.0\lib" -llibmysql
INCLUDEPATH += "C:\Program Files\MySQL\MySQL Server 8.0\include"
DEPENDPATH += "C:\Program Files\MySQL\MySQL Server 8.0\include"


include(../qsqldriverbase.pri)

```
Then build the project. Note that it is assumed that you installed `MySql server` on the `C` drive. If it's built sucessfully a directory would be created in `C:\plugins\sqldrivers` with two .dll files and two .a files inside it. Copy the two dlls into `C:\Qt\Qt5.12.4\5.12.4\[Your Toolkit name]\plugins\sqldrivers`. Then unzip [here](https://dev.mysql.com/downloads/installer/) and copy `bin/libmysql` into `C:\Qt\Qt5.12.4\5.12.4\[Your Toolkit name]\bin`.
<br>Solving the missing dynamic libraries in Qt 5.12.4 on Windows.
