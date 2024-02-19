# Nav SDK编码规范

## 注释规范-Doxygen

### 文件注释

``` C++
/**
 * @file 文件名
 * @brief 简要介绍
 */
```

### 代码注释

1. 注释在代码前方时，使用/** XXXXX */进行注释。
2. 注释在代码后方时，使用/**< XXXXX */进行注释。

``` C++
/** 类说明 */
class Afterdoc_Test
{
  public:
    /** 
     * 枚举说明
     */
    enum EnumType
    {
      int EVal1,     /**< 枚举值1说明 */
      int EVal2      /**< 枚举值2说明 */
    };

    void member();   /**< 成员函数说明 */
    
  protected:
    int value;       /**< 成员变量说明 */
};
```

### 常用属性

- brief 简要说明。
- details 详细说明。
- param[in] 参数名 参数意义（入参）。
- param[out] 参数名 参数意义（出参）。
- return 返回值说明。
- pre 代码调用前的使用条件。
- post 代码调用后的使用条件。
- par 开始一个段落，段落名描述由自己指定。
- code 代码 @endcode
- see 参考内容，将自动生成其中出现的引用链接。
- deprecated 函数废弃说明。
- warning 使用函数时必须知道的警告信息。
- exception 对异常进行注释
- remark 备注说明。
- todo 将要做的事情。将会被汇总到TODO列表。
- bug 缺陷说明。将会被汇总到BUG列表。
- note 注意事项或者重要的注解。
- retval 返回值 返回值说明。

``` C++
/**
 * 打开文件
 * 文件打开成功后，必须使用::CloseFile函数关闭
 *
 * @param[in] fileName    文件名
 * @param[in] fileMode    文件模式，可以由以下几个模块组合而成：
 *     -r读取
 *     -w 可写
 *     -a 添加
 *     -t 文本模式(不能与b联用)
 *     -b 二进制模式(不能与t联用)
 *
 * @return 返回文件编号
 *  --1表示打开文件失败(生成时:.-1)
 *
 * @note 文件打开成功后，必须使用::CloseFile函数关闭
 */
int OpenFile(const char* fileName, const char* fileMode);

```

## 编码风格规范 Coding Style

### 一、基本类型

整型数据使用标准库cstdint

- 有符号整型数据：int32_t
- 无符号整型数据：uint32_t
- 宽字符数据：wchar_t
- 窄字符数据：char

### 二、命名规范

1. 文件名全部小写，单数，下划线分隔。例如：map__view.h，map__view_impl.cpp
2. 类名采用“大驼峰”形式，首字母和单词字母均大写。例如：MapView，MapService
3. 类函数名采用“大驼峰”形式，首字母和单词字母均大写。使用动词+宾语形式命名。例如：DoRender()，GetValue()
4. 枚举名首字母大写，后缀Enum，枚举值使用全大写字母，以下划线分隔。例如：SexEnum.MALE
5. 返回bool类型的函数，以is / has / contains等，能够明确表明bool值意图的词语开头。例如：isVisible()，hasCharacter()
6. 设定，取得属性的函数统一使用setXXX(), getXXX()形式。
7. 对外接口类使用纯虚类。
8. 对外文件以ni_开头。例如：ni_map_view.h
9.  测试类，以待测试类开头，Test结尾。例如：MapViewTest
10. 增删改查等数据接口操作，使用以下动词形式。可以在动词后追加宾语。返回bool代表操作是否成功。
> 创建：Obj\* create();  
> 添加：bool add(Obj o), bool add(int index, Obj\* o);  
> 删除：bool remove(int index), bool remove(Obj\* o);  
> 更新：bool set(int index, Obj\* o);  
> 取得：Obj\* get(int index);  
> 查找：int find(*Obj o);  
> 数量：int count();  

11.  对仗词语标准
> add / remove  
> increment / decrement  
> open / close  
> begin / end  
> insert / delete  
> show / hide  
> create / destroy  
> lock / unlock  
> source / target  
> first / last  
> min / max  
> start / stop  
> set / get  
> next / previous  
> up / down  
> old / new  
> init / uninit  

12.  限定词后置。计算最大值，最小值，最佳值，平均值，总计，数量等数据时，变量以Max，Min，Best，Average，Total，Count作为结尾。例如：distanceMax，priceTotal，routeResultBest

### 三、编码风格

1. 接口设计时，尽可能通过const限制接口的使用。
2. 编译时，应当保证无WARNING信息。
3. namespace不缩进，类内public, private, protected不缩进。
4. 注释遵守doxygen的格式规范。

### 四、Git提交说明

1. 需要在include/nisdk/changelog.md中，根据更新日期，标明接口变化内容。功能实现。
2. 需要在git提交日志中，标明变更类型，变更简介，变更详情。
> feat: 新增产品功能  
> fix: 修复bug  
> docs: 文档变更  
> style: 格式调整  
> refactor: 代码重构  
> perf: 性能优化  
> test: 测试模块  
> build: 编译环境  
> revert: 代码回退
