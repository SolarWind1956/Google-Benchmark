# Google-Benchmark
How I've generated Google benchmark.lib for MS Windows with MS Visual Studio 2019 and GitHUB Google packages
09-01-21 Google Benchmark and Google Test
С GitHub я скачал два пакета benchmark-master и googletest-master. Второй, хоть и встроен в Visual Studio Communication, но без него мне не удавалось собрать первый - benchmark-master.
Содержимое папки googletest-master я вставил в каталог \benchmark\googletest, только после этого запустил CMake GUI, и все собралось.
Но были созданы только автономные модульные тесты, никаких библиотек benchmark.lib, скомпановано не было.
Тогда я вытащил в отдельный каталог 
C:\PolygonC++\GoogleBenchmark\incl_src 
все исходники статической библиотки benchmark.lib, добавил в каталог файл benchmark.h, чтобы потом не городить огород с папками (как потом выяснилось, зря, так во всех файлах пришлось исправлять 
#include "benchmark\benchmark.h" на 
#include "benchmark.h".
Сгенерировал в Visual Studio проект статической библиотеки и собрал его. Получил на выходе библиотеку benchmark.lib.
При этом необходимо следить за тем, чтобы совпадали такие параметры для целевого приложения использования, как Debug / Release и x32 / x64.
Видимо, могли бы иметь место следующие варианты библиотеки:
benchmark32.lib		- x32 Release 
benchmark64.lib		- x64 Release 
benchmark32d.lib		- x32 Debug
benchmark64d.lib		- x64 Debug 
Я ограничися одним названием benchmark.lib, но уже впадлу было переиначивать.
Теперь надо было приступать к сборке тестовой проги. Я собрал в одном проекте и Google Benchmark and Google Test, и оказалось, что Benchmark задавил Google Test.
Пришлось делать два отдельный проекта. Но это не страшно.
При сборке проекта Google Benchmark потребовалась библиотека shlwapi.lib (про библиотеку benchmark.lib - это понятно нужна). В этой библиотке вроде как функции работы с реестром MS Windows. Ссылки на обе библиотеки я вставил в поле "Дополнительные зависимости" свойств проекта "Компоновщик -> Вход". 
Доречи, библиотеку shlwapi.lib я не нашел во всем диске C:\ (может, плохо искал). Нашел, правда, ее динамический аналог shlwapi.dll. Нет желания пока разбираться в этом, да и времени нет. Подумал, что компоновщик, не найдя статическую библиотеку, взял, да и использовал динамическую. Я не знаю так хорошо всю эту кухню.
