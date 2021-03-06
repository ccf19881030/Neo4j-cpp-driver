# Neo4j-cpp-driver
C++的Neo4j驱动,该驱动基于libcurl和Neo4j的REST接口实现了C++对Neo4j的操作，具体的接口方法参照了Neo4j官方为Node.js提供的功能。

## 依赖
该驱动依赖libcurl和JsonCpp，在使用该驱动前请先安装配置好上述依赖库。
libcurl头文件在api.hpp中被引入，JsonCpp头文件在api.hpp和kit.hpp中被引入，在安装配置完依赖库后，需对应调整此处的头文件并引入库文件。

## 组成简介
该驱动包括database、api、kit和base64四个部分组成。

### database.hpp/cpp
该模块为驱动的底层模块，主要用于curl的初始化和析构时的清理操作。
<br/>`由于curl的特性，初始化部分使用了单例模式`

### api.hpp/cpp
该模块为驱动的核心部分，主要包括增删改查等各类数据库操作。

### kit.hpp/cpp
该模块中包括若干方法，主要用于解析HTTP协议头中的状态码、生成条件字符串等功能。

### base64.hpp
Neo4j在登录验证时使用了Base64编码，该组件用于对数据库连接验证时的密码进行编码处理。

## 示例
    try
    {
        //使用单例模式获得Neo4j驱动
        std::shared_ptr<neo4jDriver::Neo4j> neo4j = neo4jDriver::Neo4j::getNeo4j();
        //利用Neo4j驱动和连接参数生成API对象
        neo4jDriver::Neo4jAPI neo4jAPI(neo4j, "127.0.0.1", "7474", "neo4j", "123456");
        //连接数据库
        neo4jAPI.connectDatabase();
        
        //具体的数据库操作
        //......
        
        //断开数据库连接
        neo4jAPI.closeDatabase();
        //清理数据库驱动
        neo4j->deleteNeo4j();
    }
    catch (char* e)
    {
        std::cout << e << std::endl;
    }
    
## API
`尚未提供，请参照api.hpp`

## 许可协议
Neo4j-cpp-driver使用MIT许可证。关于Neo4j-cpp-driver依赖项的协议见对应依赖项的License文件。
