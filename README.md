# Google-Benchmark
How I've generated Google benchmark.lib for MS Windows with MS Visual Studio 2019 and GitHUB Google packages
09-01-21 Google Benchmark and Google Test
09-01-21 Google Benchmark and Google Test
I downloaded two packages benchmark-master and googletest-master from GitHub. The second, although it is built into Visual Studio Communication, but without it I could not build the first one - benchmark-master.
I pasted the contents of the googletest-master folder into the \ benchmark \ googletest directory, only after that I started CMake GUI, and everything was assembled.
But only stand-alone unit tests were created, no benchmark.lib libraries were compiled.
Then I pulled into a separate directory
C: \ PolygonC ++ \ GoogleBenchmark \ incl_src
all the sources of the benchmark.lib static library, added the benchmark.h file to the directory, so that later not to fence the garden with folders (as it turned out later, in vain, so in all files it was necessary to fix
#include "benchmark \ benchmark.h" on
#include "benchmark.h".
Generated a static library project in Visual Studio and built it. I got the benchmark.lib library at the output.
When doing this, you must ensure that the parameters for the target application of use, such as Debug / Release and x32 / x64, are the same.
Apparently, the following library options could take place:
benchmark32.lib - x32 Release
benchmark64.lib - x64 Release
benchmark32d.lib - x32 Debug
benchmark64d.lib - x64 Debug
I limited myself to one name benchmark.lib, but it was already in vapadlu to change.
Now I had to start assembling the test program. I collected both Google Benchmark and Google Test in one project, and it turned out that Benchmark crushed Google Test.
I had to do two separate projects. But that's okay.
When building the Google Benchmark project, the shlwapi.lib library was required (about the benchmark.lib library - this is clearly needed). In this library it seems like functions for working with the MS Windows registry. I pasted links to both libraries in the Additional Dependencies field of the Linker -> Input project properties.
Speech, I did not find the shlwapi.lib library in the entire C: \ drive (maybe I was looking badly). Found, however, its dynamic analogue shlwapi.dll. There is no desire to figure this out yet, and there is no time. I thought that the linker, not finding the static library, took, and used the dynamic one. I don't know this whole kitchen that well.
