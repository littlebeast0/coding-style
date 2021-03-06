# 1 变量命名
## 1.1 糟糕的变量命名策略
### 1.1.1 类的成员变量用m\_来区分是不是一个好的方法？
不是。我们在类成员变量命名中使用一个前缀，是为了将类成员变量跟其它局部变量区别开来。在变量命名中，我们要用尽量少的符号来达到我们的目的。m_使用了两个符号，理论上这不是一个很好的美观的方式。mXXX的方式都比m_好得多。但mXXX的方式的缺点在于后一个字幕必须大小写，输入大写字幕时需要多按一次cap键。
推荐使用_XXX的方式。这种方式下，变量后面的名称可以不用担心大小写问题，不会使用过多的符号，简洁优雅。

### 1.1.2 变量前用i,u,l,f等字母来彰显变量类型是不是一个好的方法？
不是。分两个方面阐述。
首先，对C/C++这种强类型预言，变量使用前必须要先声明，必须要指定变量类型，如果代码是自己写的，那么变量的类型自己肯定会记得很清楚。如果代码自己维护的，那么对C/C++而言，依赖SourceInsight可以很清晰的解析显示变量的类型。
其次，一个变量的命名，表意更为重要。不论是阅读代码还是书写代码，表意的变量名对表达逻辑更加重要，类型反而显得不那么重要了。
综上亮点，变量前用i,u,l,f等字母来彰显变量类型并不是一个很好的设计。不推荐使用这种命名方式。

## 1.2 推荐的命名方式
+ 类变量的命名，推荐只使用_作为前缀来标识即可。或者可以不用.
+ 类名、函数名使用camel-case方式进行命名。如果函数中有大写缩略词，则可以用下划线进行区分。函数单个词则可以首字母小写。
+ struct 定义的结构体，一律使用St开头命令。
+ 文件名使用camel-case命名，如果文件只有一个类，那类名要与文件名一致

# 2 判断表达式
## 2.1 指针、整型、浮点型、字符串、bool值的比较方式
### 2.1.1 糟糕的写法
```c++
if(val)  {
    ...
}
```
这种写法编译器是可以正常识别，但是指针、整型、bool值、字符串、浮点数严格意义上来说是不同的类型。if(val)的写法会隐藏掉val本身的类型信息，这对我们阅读代码时眼睛parse代码时很不利的。

### 2.1.2 正确的写法
指针：if(val != NULL) 或者 if(val == NULL)  
整型：if(val != 0) 或者 if(val == 10)  
bool值：if( val == true) 或者 if(val == false)  
字符串：if(val != "" ) 或者 if(val == "")  
浮点值：if( abs(val) < MIN_PRECISION )  

## 2.2 避免多层if的深度嵌套
### 2.2.1 两种写法
多层if else 嵌套时，有两种写法。
写法1：不断在正确的case中进行进一步的逻辑操作
```c++
if(correct_case1)
{
    if(correct_case2)
    {
        ...
    }
    else
    {
    
    }
}
else
{

}
```
写法2：采用guard clause,先判定错误的case，一旦遇到错误的case就返回。最后才处理正确的case。
```c++
if(wrong_case1)
{
    // LOG
    return;
}

if(wrong_case2)
{
    // LOG
    return;
}
....
if(wrong_caseN)
{
    // LOG
    return;
}
// code of correct case
```
这两种写法只是表达方式的不同，但是在代码的可读性和优雅性上是有区别的。
写法一会造成if else语句的深度嵌套，这会导致代码非常难以阅读理解。
写法二避免了写法1的问题。
一般来说，if else嵌套最多不要超过4层。太多了就会导致代码非常难以理解。

## 3 misc
### 3.1 头文件包含
头文件包含，系统头文件统一放在自定义头文件前面。

### 3.2 注释正文跟注释符无比要空一格
正确的写法： // TODO:
错误的写法： //TODO:

### 3.3 git commit日志格式要统一
提交日志格式统一约定为 [fix/feature](mod1, mod2, ..., modN) 1.aaaa 2.bbbb
如果系统中没有多个模块，则mod块部分可以不写。
