# 第二章 实训二  RISC-V下Makefile使用


## 前言

Linux 环境下的程序员如果不会使用GNU make来构建和管理自己的工程，应该不能算是一个合格的专业程序员，至少不能称得上是 Unix程序员。在Linux或Unix环境下，对于只含有几个源代码文件的小程序（如hello.c）的编译，可以手工键入gcc命令对源代码文件逐个进行编译；然而在大型的项目开发中，可能涉及几十到几百个源文件，采用手工键入的方式进行编译，则非常不方便，而且一旦修改了源代码，尤其头文件发生了的修改，采用手工方式进行编译和维护的工作量相当大，而且容易出错。所以在Linux或Unix环境下，人们通常利用GNU make工具来自动完成应用程序的维护和编译工作。在 Linux（unix ）环境下使用GNU 的make工具能够比较容易的构建一个属于你自己的工程，整个工程的编译只需要一个命令就可以完成编译、连接以至于最后的执行。不过这需要我们投入一些时间去完成一个或者多个称之为Makefile 文件的编写。

Makefile是按照某种脚本语法编写的文本文件，而GNU make能够对Makefile中指令进行解释并执行编译操作。Makefile文件定义了一系列的规则来指定哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至于进行更复杂的功能操作。所要完成的Makefile 文件描述了整个工程的编译、连接等规则。其中包括：工程中的哪些源文件需要编译以及如何编译、需要创建那些库文件以及如何创建这些库文件、如何最后产生我们想要的可执行文件。尽管看起来可能是很复杂的事情，但是为工程编写Makefile 的好处是能够使用一行命令来完成“自动化编译”，一旦提供一个（通常对于一个工程来说会是多个）正确的 Makefile。编译整个工程你所要做的唯一的一件事就是在shell 提示符下输入make命令。整个工程完全自动编译，极大提高了效率。

make命令执行时，需要一个 Makefile 文件，以告诉make命令需要怎么样的去编译和链接程序。我们要写一个Makefile来告诉make命令如何编译和链接文件。我们的规则是：

1. 如果这个工程没有编译过，那么我们的所有C文件都要编译并被链接。
2. 如果这个工程的某几个C文件被修改，那么我们只编译被修改的C文件，并链接目标程序。
3. 如果这个工程的头文件被改变了，那么我们需要编译引用了这几个头文件的C文件，并链接目标程序。

只要我们的Makefile写得够好，所有的这一切，我们只用一个make命令就可以完成，make命令会自动智能地根据当前的文件修改的情况来确定哪些文件需要重编译，从而自己编译所需要的文件和链接目标程序。
GNU make工作时的执行步骤如下：

1. 读入所有的Makefile。
2. 读入被include的其它Makefile。
3. 初始化文件中的变量。
4. 推导隐晦规则，并分析所有规则。
5. 为所有的目标文件创建依赖关系链。
6. 根据依赖关系，决定哪些目标要重新生成。
7. 执行生成命令。

1-5步为第一个阶段，6-7为第二个阶段。

第一个阶段中，如果定义的变量被使用了，那么，make会把其展开在使用的位置。但make并不会完全马上展开，make使用的是拖延战术，如果变量出现在依赖关系的规则中，那么仅当这条依赖被决定要使用了，变量才会在其内部展开。下面对Makefile的相关问题进行简单介绍：

Makefile文件由一组依赖关系和规则构成。

Makefile的依赖关系：

依赖关系定义了最终应用程序里的每个文件与源文件之间的关系。每个依赖关系由一个目标和一组该目标所依赖的源文件组成。规则则描述了如何通过这些依赖关系创建目标。依赖关系的写法如下：先写目标的名称，后面紧跟着一个冒号，接着是空格或制表符，最后是用空格或制表符隔开的文件列表，如：

    myapp：main.o my.o
    
    main.o: main.c a.h
    
    my.o: my.c b.h

它表示目标myapp依赖于main.o和my.o，而main.o依赖于main.c和a.h，等等。这组依赖关系形成一个层次结构，它显示了源文件之间的关系，如果a.h发生了变化，就需要重新编译main.o。

Makefile的规则：

    arget ... : prerequisites ... 
    
            command 

target也就是一个目标文件，可以是Object File，也可以是执行文件。prerequisites就是，要生成那个target所需要的文件或是目标。 command也就是make需要执行的命令。（任意的Shell命令）command一定要以Tab键开始，否者编译器无法识别command 

这是一个文件的依赖关系，也就是说，target这一个或多个的目标文件依赖于prerequisites中的文件，其生成规则定义在command中。说白一点就是说，prerequisites中如果有一个以上的文件比target文件要新的话，command所定义的命令就会被执行。这就是Makefile的规则。也就是Makefile中最核心的内容。
一个简单的Makefile文件：

    myapp: main.o my.o
    
    gcc –o myapp main.o my.o
    
    main.o: main.c a.h
    
    gcc –c main.c 
    
    my.o : my.c b.h
    
    gcc –c my.c 
    
    clean:
    
    rm myapp main.o my.o

在这个makefile中，目标文件（target）包含：执行文件myapp和中间目标文件（*.o），依赖文件（prerequisites）就是冒号后面的那些 .c 文件和 .h文件。每一个 .o 文件都有一组依赖文件，而这些 .o 文件又是执行文件 myapp的依赖文件。依赖关系的实质上就是说明了目标文件是由哪些文件生成的，换言之，目标文件是哪些文件更新的。 

在定义好依赖关系后，后续的那一行定义了如何生成目标文件的操作系统命令，一定要以一个Tab键作为开头。记住，make并不管命令是怎么工作的，他只管执行所定义的命令。make会比较targets文件和prerequisites文件的修改日期，如果prerequisites文件的日期要比targets文件的日期要新，或者target不存在的话，那么，make就会执行后续定义的命令。 

这里要说明一点的是，clean不是一个文件，它只不过是一个动作名字，有点像C语言中的lable一样，其冒号后什么也没有，那么，make就不会自动去找文件的依赖性，也就不会自动执行其后所定义的命令。要执行其后的命令，就要在make命令后明显得指出这个lable的名字。这样的方法非常有用，我们可以在一个makefile中定义不用的编译或是和编译无关的命令，比如程序的打包，程序的备份，等等。

make是如何工作的

在默认的方式下，也就是我们只输入make命令。那么
1. make会在当前目录下找名字叫“Makefile”或“makefile”的文件。
2. 如果找到，它会找文件中的第一个目标文件（target），在上面的例子中，他会找到“myapp”这个文件，并把这个文件作为最终的目标文件。
3. 如果myapp文件不存在，或是myapp所依赖的后面的 .o 文件的文件修改时间要比myapp这个文件新，那么，他就会执行后面所定义的命令来生成myapp这个文件。
4. 如果myapp所依赖的.o文件也存在，那么make会在当前文件中找目标为.o文件的依赖性，如果找到则再根据那一个规则生成.o文件。（这有点像一个堆栈的过程）
5. 当然，你的C文件和H文件是存在的啦，于是make会生成 .o 文件，然后再用 .o 文件生成make的终极任务，也就是执行文件myapp了。



## 任务

1. 创建hello.c文件，编写一个简单的helloworld程序

2. 使用命令行的方法手动编译hello.c文件

3. 查询Makefile的相关资料，自主学习Makefile的基本书写规则

4. 编写hello.c文件的Makefile文件，并使用命令生成可执行文件


参考答案：


    #include <stdlib.h>
       
    int main()
    {
      printf("hello.world!\n");
      return 0;
    }
    makefile
    hello : hello.o
       cc -o hello hello.o
    hello.o : hello.c
       cc -c hello.c -o hello.o
    clean :
       rm -f hello.o
