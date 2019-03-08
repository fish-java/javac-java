## 编译到指定文件夹
之前我们使用javac都是就地编译的，编译后的文件和源文件都是在同一个目录下，这样是很不美观的。我们可以给

创建下面的目录结构
```
.
├── Main.java
├── README.md
└── com
    └── github
        └── Bird.java
```

假如我们想把结果编译到`./dist`目录下，我们可以：
```
javac -d ./dist Main.java
```
通过 `-d` 来指明输出目录