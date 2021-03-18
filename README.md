## Spring Native


## Prerequisites


- [GraalVM](https://github.com/graalvm/graalvm-ce-builds)
    ```
    > java -version
    openjdk version "11.0.10" 2021-01-19
    OpenJDK Runtime Environment GraalVM CE 21.0.0.2 (build 11.0.10+8-jvmci-21.0-b06)
    OpenJDK 64-Bit Server VM GraalVM CE 21.0.0.2 (build 11.0.10+8-jvmci-21.0-b06, mixed mode, sharing)
    ```
-   JAVA_HOME point to GraalVM
    - MacOS: export JAVA_HOME=/path/to/graalvm/Contents/Home
    - Windows: set JAVA_HOME=c:\path\to\graalvm
    - Linux: export JAVA_HOME=/path/to/graalvm
-   PATH variable contains GraalVM bin folder
    - MacOS: export PATH=$JAVA_HOME/bin:$PATH
    - Windows: set JAVA_HOME=%JAVA_HOME%\bin;%PATH$
    - Linux: export JAVA_HOME=$JAVA_HOME/bin:$PATH   
-   [GraalVM Native Image](https://docs.spring.io/spring-native/docs/current/reference/htmlsingle/#getting-started-native-image)
    ```
    > gu install native-image
    ```
-   Clone this repository
    ```
    git clone http://github.com/yogendra/native-spring-workshop.git native-spring-workshop
    ```



## GraalVM Examples

[Source: GraalVM Documentation](https://www.graalvm.org/examples/java-performance-examples/)

### Simple upper case counter

**Directory:** examples/CountUppercase

 -  Lets compile it first

    ```
    javac -d out CountUppercase.java
    ```

-   This produced `CountUppercase.class` in same directory. We can run this using following command.

    ```
    java -cp out CountUppercase
    ```
    **Output**:
    ```
    1 (380 ms)
    2 (288 ms)
    3 (243 ms)
    4 (260 ms)
    5 (285 ms)
    6 (238 ms)
    7 (235 ms)
    8 (240 ms)
    9 (253 ms)
    total: 69999993 (2655 ms)
    ```

-   You can see the compilation time using follwing command
    ```
    java -cp out -Dgraal.PrintCompilation=true CountUppercase 
    ```
    **Output**:
    ```
    [Use -Dgraal.LogFile=<path> to redirect Graal log output to a file.]
    HotSpotCompilation-177         Ljava/lang/Object;                                                     <init>                                        ()V                                                 | 11405us     2B bytecodes    91B codesize
    HotSpotCompilation-260         Ljava/util/stream/AbstractPipeline;                                    wrapSink                                      (Ljava/util/stream/Sink;)Ljava/util/stream/Sink;    | 12779us   204B bytecodes   542B codesize
    HotSpotCompilation-244         Ljava/lang/StringLatin1$CharsSpliterator;                              forEachRemaining                              (Ljava/util/function/IntConsumer;)V                 | 6242us   886B bytecodes   914B codesize
    HotSpotCompilation-271         Ljava/util/stream/IntPipeline$9;                                       opWrapSink                                    (ILjava/util/stream/Sink;)Ljava/util/stream/Sink;   | 1775us   102B bytecodes   338B codesize
    HotSpotCompilation-261         Ljava/util/stream/AbstractPipeline;                                    evaluate                                      (Ljava/util/stream/TerminalOp;)Ljava/lang/Object;   | 20356us  2597B bytecodes  2450B codesize
    HotSpotCompilation-182         Ljava/lang/CharacterData;                                              of                                            (I)Ljava/lang/CharacterData;                        |  707us   240B bytecodes   102B codesize
    HotSpotCompilation-191         LCountUppercase$$Lambda$14/603742814;                                  test                                          (I)Z                                                | 1803us   666B bytecodes   242B codesize
    HotSpotCompilation-192         Ljava/util/stream/IntPipeline$9$1;                                     accept                                        (I)V                                                | 2944us   742B bytecodes   498B codesize
    HotSpotCompilation-193         Ljava/lang/CharacterDataLatin1;                                        isUpperCase                                   (I)Z                                                | 1031us    62B bytecodes   185B codesize
    HotSpotCompilation-195         Ljava/lang/CharacterDataLatin1;                                        isOtherUppercase                              (I)Z                                                | 1045us    58B bytecodes   198B codesize
    HotSpotCompilation-178         Ljava/util/Objects;                                                    requireNonNull                                (Ljava/lang/Object;)Ljava/lang/Object;              |  580us    28B bytecodes    82B codesize
    HotSpotCompilation-196         Ljava/util/stream/ReduceOps$CountingSink$OfInt;                        accept                                        (I)V                                                |  390us    22B bytecodes   108B codesize
    HotSpotCompilation-226         Ljava/util/stream/AbstractPipeline;                                    isParallel                                    ()Z                                                 |  491us    16B bytecodes   150B codesize
    HotSpotCompilation-183         Ljava/lang/String;                                                     isLatin1                                      ()Z                                                 |  669us    38B bytecodes   154B codesize
    HotSpotCompilation-250         Ljava/lang/invoke/Invokers$Holder;                                     linkToTargetMethod                            (Ljava/lang/Object;)Ljava/lang/Object;              | 1330us    16B bytecodes   140B codesize
    HotSpotCompilation-251         Ljava/lang/invoke/DirectMethodHandle$Holder;                           getObject                                     (Ljava/lang/Object;)Ljava/lang/Object;              | 10385us    68B bytecodes   442B codesize
    HotSpotCompilation-252         Ljava/util/stream/AbstractPipeline;                                    <init>                                        (Ljava/util/stream/AbstractPipeline;I)V             | 4239us   260B bytecodes  1010B codesize
    HotSpotCompilation-253         Ljava/util/stream/StreamOpFlag;                                        fromCharacteristics                           (Ljava/util/Spliterator;)I                          | 1319us    84B bytecodes   157B codesize
    HotSpotCompilation-254         Ljava/util/stream/AbstractPipeline;                                    <init>                                        (Ljava/util/Spliterator;IZ)V                        | 2796us   115B bytecodes   700B codesize
    HotSpotCompilation-266         Ljava/lang/String;                                                     chars                                         ()Ljava/util/stream/IntStream;                      | 6045us   435B bytecodes   690B codesize
    HotSpotCompilation-268         Ljava/util/stream/IntPipeline;                                         filter                                        (Ljava/util/function/IntPredicate;)Ljava/util/stream/IntStream;  | 4016us   177B bytecodes   374B codesize
    HotSpotOSRCompilation-279      LCountUppercase;                                                       main                                          ([Ljava/lang/String;)V                             (OSR@61)  | 25972us  1780B bytecodes  4658B codesize
    HotSpotCompilation-269         Ljava/util/stream/IntPipeline;                                         count                                         ()J                                                 | 2399us    66B bytecodes   402B codesize
    HotSpotCompilation-267         Ljava/lang/StringLatin1$CharsSpliterator;                              <init>                                        ([BIII)V                                            | 1880us    72B bytecodes   352B codesize
    HotSpotCompilation-243         Ljava/util/stream/Sink;                                                end                                           ()V                                                 |  285us     2B bytecodes    91B codesize
    HotSpotCompilation-262         Ljava/util/stream/AbstractPipeline;                                    sourceSpliterator                             (I)Ljava/util/Spliterator;                          | 1954us   607B bytecodes   370B codesize
    HotSpotCompilation-263         Ljava/util/stream/AbstractPipeline;                                    wrapAndCopyInto                               (Ljava/util/stream/Sink;Ljava/util/Spliterator;)Ljava/util/stream/Sink;  | 10653us  1576B bytecodes  1426B codesize
    HotSpotCompilation-264         Ljava/util/stream/AbstractPipeline;                                    copyInto                                      (Ljava/util/stream/Sink;Ljava/util/Spliterator;)V   | 7187us  1308B bytecodes  1010B codesize
    HotSpotCompilation-265         Ljava/util/Spliterator;                                                getExactSizeIfKnown                           ()J                                                 | 1029us    82B bytecodes   198B codesize
    HotSpotCompilation-245         Ljava/util/stream/ReduceOps$9;                                         getOpFlags                                    ()I                                                 |  255us     8B bytecodes    96B codesize
    HotSpotCompilation-246         Ljava/lang/StringLatin1$CharsSpliterator;                              estimateSize                                  ()J                                                 |  359us    22B bytecodes   102B codesize
    HotSpotCompilation-247         Ljava/util/stream/ReduceOps$CountingSink;                              begin                                         (J)V                                                |  314us    12B bytecodes   102B codesize
    HotSpotCompilation-270         Ljava/util/stream/ReduceOps$9;                                         evaluateSequential                            (Ljava/util/stream/PipelineHelper;Ljava/util/Spliterator;)Ljava/lang/Object;  | 15755us  1786B bytecodes  2098B codesize
    HotSpotCompilation-272         Ljava/util/stream/IntPipeline$9$1;                                     begin                                         (J)V                                                | 1139us    38B bytecodes   213B codesize
    HotSpotCompilation-273         Ljava/util/Spliterator$OfInt;                                          forEachRemaining                              (Ljava/util/function/Consumer;)V                    | 7528us   992B bytecodes   951B codesize
    HotSpotCompilation-274         Ljava/util/stream/Sink$ChainedInt;                                     end                                           ()V                                                 |  748us    22B bytecodes   210B codesize
    HotSpotCompilation-275         Ljava/util/stream/ReduceOps$CountingSink$OfInt;                        get                                           ()Ljava/lang/Object;                                | 1174us    18B bytecodes   358B codesize
    HotSpotCompilation-276         Ljava/lang/Long;                                                       valueOf                                       (J)Ljava/lang/Long;                                 | 1038us    80B bytecodes   151B codesize
    HotSpotCompilation-289         Ljava/lang/String;                                                     hashCode                                      ()I                                                 | 1284us   136B bytecodes   294B codesize
    HotSpotCompilation-307         Ljava/lang/String;                                                     charAt                                        (I)C                                                | 1316us   144B bytecodes   255B codesize
    HotSpotCompilation-309         Ljava/lang/StringLatin1;                                               equals                                        ([B[B)Z                                             | 1671us    72B bytecodes   306B codesize
    1 (333 ms)
    HotSpotCompilation-317         Ljava/util/HashMap;                                                    resize                                        ()[Ljava/util/HashMap$Node;                         | 16879us   712B bytecodes  3698B codesize
    HotSpotCompilation-318         Ljava/lang/StringLatin1;                                               hashCode                                      ([B)I                                               | 3970us    84B bytecodes   469B codesize
    HotSpotOSRCompilation-334      LCountUppercase;                                                       main                                          ([Ljava/lang/String;)V                             (OSR@61)  | 29429us  1787B bytecodes  7474B codesize
    HotSpotCompilation-319         Ljava/util/HashMap;                                                    putVal                                        (ILjava/lang/Object;Ljava/lang/Object;ZZ)Ljava/lang/Object;  | 17101us   952B bytecodes  3730B codesize
    2 (141 ms)
    3 (87 ms)
    4 (145 ms)
    5 (89 ms)
    6 (87 ms)
    7 (88 ms)
    8 (126 ms)
    9 (84 ms)
    total: 69999993 (1263 ms)    
    ```

-   Now lets just run the same code without GraavVM compilation, just the regular JVM

    ```
    java java -cp out -XX:-UseJVMCICompiler CountUppercase
    ```
    **Output**:
    ```
    1 (240 ms)
    2 (113 ms)
    3 (80 ms)
    4 (182 ms)
    5 (85 ms)
    6 (80 ms)
    7 (78 ms)
    8 (74 ms)
    9 (145 ms)
    total: 69999993 (1162 ms)
    ```
-   Make a native binary (Windows and Linux only)
    ```
    native-image --static -cp out CountUppercase out/count-uppercase
    ```
    **Output:**
    ```

    ```
-   Run native image
    ```
    out/count-uppercase
    ```
    **Output:**
    ```
    
    ```

### Blender

**Directory:** examples/Blender

-   Compile `Blender.java`
    ```
    javac -d out Blender.java
    ```
-   Run `Blender` with GraalVM
    ```
    java -cp out Blender
    ```
    **Output**:
    ```
    949 ms
    912 ms
    907 ms
    912 ms
    945 ms
    963 ms
    967 ms
    997 ms
    1309 ms
    971 ms
    ```
-   Run `Blender` without GraalVM
    ```
    java -cp out -XX:-UseJVMCICompiler Blender
    ```
    **Output**:
    ```
    1528 ms
    1190 ms
    1193 ms
    1208 ms
    1181 ms
    1381 ms
    1191 ms
    1339 ms
    1287 ms
    1159 ms
    ```

-   Make a native binary (Windows and Linux only)
    ```
    native-image --static -cp out Blender out/blender
    ```
    **Output:**
    ```

    ```
-   Run native image
    ```
    out/blender
    ```
    **Output:**
    ```
    
    ```
## Native Image with GraalVM

**Directory:** examples/HelloWorld

Lets build a docker image with a native binary. Nothing big, just a simple "Hellow, World!"

```
make demo
```

## Spring Native

[Source: ]
