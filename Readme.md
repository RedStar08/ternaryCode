## 编译原理课程设计

+ My Principles of compilation cource job a LR(1) compiler translate arithmetic expression to ternary code

#### 说明

+ 将算术表达式翻译成三地址代码

+ 采用LR(1) 语法分析器进行语法分析

+ 在归约阶段，遇到包含算术表达式的产生式时，立刻发射一条三地址代码

  #### S-属性文法

|  产生式   |                           语义规则                                                        |
| :------:  | :----------------------------------------------------------:                              |
| S -> i=E  |         S.code = E.code \|\| gen(i.place‘=’E.place);                                      |
| E -> E+T  | E.code = E.code \|\| T.code \|\| gen(newplace‘=’E.place‘+’T.place); E.place = newplace;   |
| E -> E-T  | E.code = E.code  \|\| T.code  \|\| gen(newplace‘=’E.place‘-’T.place); E.place = newplace; |
|  E -> T   |             E.code = T.code; E.place = T.place;                                           |
| T -> T\*F | T.code = T.code \|\| F.code \|\| gen(newplace‘=’T.place‘*’F.place); T.place = newplace;   |
| T -> T/F  | T.code = T.code \|\| F.code \|\| gen(newplace‘=’T.place‘/’F.place); T.place = newplace;   |
|  T -> F   |             T.code = F.code; T.place = F.place;                                           |
| F -> (E)  |             F.code = E.code; F.place = E.place;                                           |
|  F -> i   |  F.code = “”; F.place = i.place(自身符号);                                                |

