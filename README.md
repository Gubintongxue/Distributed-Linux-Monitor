分布式Linux性能分析监控

技术栈：c++，c++常用特性，docker，grpc，proto，cmake，qt

项目简介：

1、docker模块：dockerfile指定相应的cmake，grpc，proto等源码和依赖，构建整个项目环境，易于在多台服务器上部署环境，并编写容器操作的脚本指令，易于启动操作项目所依赖的环境。

2、monitor模块：采用工厂方法，通过构造moniotr的抽象类定义接口，后实现相应的CPU状态，系统负载，软中断，mem，net监控，易于为之后扩展更多系统监控；并为了模拟出真实的性能问题，使用stress工具进行模拟压测，分析相应时刻服务器的cpu状况和中断状况。

3、通过grpc框架，构建出相应的server，client；server在所要监控的服务器部署，client生成库供monitor模块和display模块调用，并考虑为了降低耦合性，项目每个模块相互独立，可拆解，只通过调用grpc服务来进行远程连接。

4、使用protobuf序列化协议，构建出整个项目的数据结构。

5、display模块分为两大部分：ui界面的构造，datamodel构造；

ui界面使用QWidget、QTableView、QStackedLayout、QPushButton等进行构建

datamodel：通过继承QAbstractTableModel，构建出相应的cpu_model、softirq_model、mem_model等，每3秒刷新一次数据。
