# Kotlin compiler performance

## On Windows

Executing on Windows in Cygwin as there's no standard time measurement method in Windows `cmd`.

````code
fun main() {
    println("Hello world!")
}
````

````code
class Performance {
    public static void main(String... args) {
        System.out.println("Hello world!");
    }
}
````

````shell
$ touch performance.kt

$ time kotlinc performance.kt

real    0m4.678s
user    0m0.030s
sys     0m0.075s

$ touch Performance.java

$ time javac Performance.java

real    0m0.616s
user    0m0.000s
sys     0m0.000s
````

We see `kotlinc` works definitely mush slower than `javac`.

The both programs work relatively equally fast:

````shell
$ time java PerformanceKt
Hello world!

real    0m0.092s
user    0m0.000s
sys     0m0.000s

$ time java Performance
Hello world!

real    0m0.095s
user    0m0.000s
sys     0m0.015s
```` 

Let's look at the compilers versions:

````shell
$ time kotlinc -version
info: kotlinc-jvm 1.4.31 (JRE 1.8.0_05-b13)

real    0m3.167s
user    0m0.045s
sys     0m0.075s

$ time javac -version
javac 1.8.0_05

real    0m0.189s
user    0m0.000s
sys     0m0.000s
````

So even `kotlinc -version` takes about 3 sec.

## On Linux

The sample code is the same (see above).

````shell
$ uname --all
Linux <hostname> 5.4.0-70-generic #78~18.04.1-Ubuntu SMP Sat Mar 20 14:10:07 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux

$ export JAVA_OPTS="--add-opens java.base/java.util=ALL-UNNAMED"

$ time kotlinc -version
info: kotlinc-jvm 1.4.31 (JRE 11.0.10+9-Ubuntu-0ubuntu1.18.04)

real    0m2,091s
user    0m3,768s
sys     0m0,221s

$ time javac -version
javac 11.0.10

real    0m0,178s
user    0m0,258s
sys     0m0,014s

~$ cd ~/kotlin_starter/performance

$ touch performance.kt
$ time kotlinc performance.kt

real    0m3,326s
user    0m7,506s
sys     0m0,307s

$ touch Performance.java
$ time javac Performance.java

real    0m0,595s
user    0m1,350s
sys     0m0,050s

$ time java PerformanceKt
Hello world!

real    0m0,062s
user    0m0,056s
sys     0m0,009s

$ time java Performance
Hello world!

real    0m0,065s
user    0m0,058s
sys     0m0,011s
````

So the same problem is on Linux.
