#Compiling a linux-qt wallet

In this guide a linux-qt wallet will be built from the sources. 

##Prerequisities

- Source codes of your coin
- A working linux (preferable 64-bit Ubuntu) distribution


##Installing the dependencies
    sudo apt-get install build-essential libboost-all-dev libcurl4-openssl-dev libdb5.1-dev libdb5.1++-dev qt-sdk make

## Check the bitcoin-qt.pro file
Before compiling the wallet let's check that the bitcoin-qt.pro file is targeted for a linux platform. If there are any windows specific dependencys you should remove/change them.

    gedit bitcoin-qt.pro

Here are the first few lines of the bitcoin-qt.pro where the dependecies are declared. It should look something like this if targeted for linux:

    TEMPLATE = app
    TARGET = litecoin-qt
    macx:TARGET = "Litecoin-Qt"
    VERSION = 0.8.6.2
    INCLUDEPATH += src src/json src/qt
    QT += network
    greaterThan(QT_MAJOR_VERSION, 4): QT += widgets
    DEFINES += QT_GUI BOOST_THREAD_USE_LIB BOOST_SPIRIT_THREADSAFE
    CONFIG += no_include_pwd
    CONFIG += thread
    
    # for boost 1.37, add -mt to the boost libraries
    # use: qmake BOOST_LIB_SUFFIX=-mt
    # for boost thread win32 with _win32 sufix
    # use: BOOST_THREAD_LIB_SUFFIX=_win32-...
    # or when linking against a specific BerkelyDB version: BDB_LIB_SUFFIX=-4.8
    
    # Dependency library locations can be customized with:
    #BOOST_INCLUDE_PATH, BOOST_LIB_PATH, BDB_INCLUDE_PATH,
    #BDB_LIB_PATH, OPENSSL_INCLUDE_PATH and OPENSSL_LIB_PATH respectively
    
    OBJECTS_DIR = build
    MOC_DIR = build
    UI_DIR = build

##Compile!

    qmake
    make

##Start the wallet

    ./litecoin-qt
    
## To mine (make money!), go to help -> debug window, and type:
  
    setgenerate true
    
## You will see your money just in about 10 minutes!
