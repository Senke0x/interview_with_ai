# 知识记录
- 在网上找到对应的blog，自己看一遍
- 将网址给到 o1 ，o1 会根据网址生成对应的知识总结
- 自己将总结抄录，可以再补充一些新的理解
- 最终将结果给到 o1 ，o1 会根据结果进行评价或者补全

## 0205 JAVA 基础知识
- 目录 https://www.cnblogs.com/skywang12345/archive/2013/06/14/index.html
- Java 的 equal 和 == 和 hashcode 的区别
    - https://www.cnblogs.com/skywang12345/p/3324958.html
- Java 的comparable 和 comparator 的区别
    - https://www.cnblogs.com/skywang12345/p/3324788.html  
- Java 的 annotation
    - https://www.cnblogs.com/skywang12345/p/3344137.html
- Java 的几种引用
    - https://www.cnblogs.com/skywang12345/p/3154474.html

# 1. 知识点总结
下面按照四个主要主题进行梳理。

## 1.1 Java 中 equals、== 和 hashCode 的区别
**来源链接:**  
• equals 和 == 与 hashCode 的区别 → https://www.cnblogs.com/skywang12345/p/3324958.html

**主要内容:**

### == 运算符
- 用于比较两个对象在内存中的地址是否相同，或者比较基本数据类型的数值是否相等。
- 对于**引用类型**，== 比较的是引用地址；对于**基本类型**，== 比较的是值。

### equals(Object obj) 方法
- 位于 **Object 类**中，默认实现是比较引用地址是否相同。
- **String**、**包装类** (Integer 等) 以及**自定义类**通常会重写 equals 方法，用于比较"内容"是否相等。
- 常见类如 String 重写 equals，以比较字符串的字面值。

### hashCode() 方法
- 也位于 **Object** 中，一般与 equals 方法共同使用，主要用于在**哈希结构**（如 HashMap、HashSet）中快速检索对象。
- 当两个对象通过 equals 方法判断相等时，二者的 hashCode 通常应相同；但 hashCode 相同并不一定代表 equals 为 true。

## 1.2 Comparable 和 Comparator 的区别
**来源链接:**  
• Comparable 和 Comparator → https://www.cnblogs.com/skywang12345/p/3324788.html

**主要内容:**

### Comparable 接口
- 在 **java.lang** 包下，内部只有一个 **compareTo(T o)** 方法。
- 若一个类实现了 Comparable，那么该类实例可以"自身"完成排序逻辑（自然顺序），在排序时无需另行指定比较器。
- 适用于一个类有"唯一固定"的排序规则场景。

### Comparator 接口
- 位于 **java.util** 包下，主要有 **compare(T o1, T o2)** 方法。
- 当无法修改目标类源码，或需要为同一类制定多种不同的排序方式时，可以使用 Comparator 来进行外部排序。
- 适用于排序规则多样化的需求场景。

## 1.3 Java 注解 (Annotation)
**来源链接:**  
• Annotation → https://www.cnblogs.com/skywang12345/p/3344137.html

**主要内容:**

### Annotation 的简介与作用
- **Java 5** 引入，用于在代码中添加元信息，如 **@Override**、**@Deprecated**、**@SuppressWarnings** 等。
- 由编译器或运行时工具读取，用来执行相应的处理或检查。

### Annotation 的分类
1. **内置注解**：@Override、@Deprecated、@SuppressWarnings 等。
2. **元注解**：@Retention、@Target、@Documented、@Inherited等，用于修饰自定义注解的作用范围和保留策略。
3. **自定义注解**：开发者自行编写，配合反射等机制，可以在编译期或运行期执行特定逻辑。

### 保留策略 (RetentionPolicy)
1. **SOURCE**：注解只在源码中存在，编译后会被丢弃。
2. **CLASS**：注解存储于 class 文件，但 JVM 加载时不会保留（默认）。
3. **RUNTIME**：JVM 加载后仍可通过反射获取，是最常见的注解保留方式。

## 1.4 Java 中的几种引用
**来源链接:**  
• Java 的几种引用 → https://www.cnblogs.com/skywang12345/p/3154474.html

**主要内容:**

### 强引用（Strong Reference）
- 程序中普遍使用的引用形式，如 new 出来的对象赋给某个变量。
- 只要强引用还在，GC 不会回收对象。

### 软引用（Soft Reference）
- 对象在内存不足时才会被 GC 回收，常用于缓存场景。
- 适合对一些可能占用较大资源、但又可以在 GC 压力较大时释放的对象进行缓存。

### 弱引用（Weak Reference）
- 一旦发生 GC，无论内存是否紧张，都可被回收。
- 常用于"只要不使用就可快速回收"的场合，例如 **WeakHashMap**。

### 虚引用（Phantom Reference）
- 无法通过它来获取对象引用，主要配合 **ReferenceQueue** 在对象被回收前做一些处理。
- 一般用于管理直接内存或元数据回收等较底层的场景。

# 2. 常见面试题问答 (Q/A)
以下基于上述知识点，整理出常见面试问题及简单回答示例。

## Q1: "==" 与 "equals" 的区别是什么？hashCode 又与 equals 有什么关系？
**A1:**
- "==" 用于比较基本类型数值或对象引用是否指向同一内存地址；而 equals 通常用来比较对象内容是否相等（需重写 equals 以作内容比较）。
- hashCode 与 equals 密切相关：如果两个对象通过 equals 判断相等，那么它们的 hashCode 应当相同；但 hashCode 相同的对象不一定 equals 相等。常见容器（HashMap、HashSet）会先比较 hashCode，再在必要时比较 equals。

## Q2: 在什么情况下需要重写 equals 和 hashCode 方法？
**A2:**
- 当自定义类需要基于业务逻辑比较"内容相等"时（而不仅仅是引用相等），就应该重写 equals，同时配套重写 hashCode。
- 例如，需要将该对象作为 **HashMap** 或 **HashSet** 的键时，一定要保证 consistent（equals 相同时 hashCode 相同）。

## Q3: Comparable 和 Comparator 的区别与最佳使用时机是什么？
**A3:**
- 实现 **Comparable** 接口的类会自身提供一个"自然顺序"，适用于有固定排序场景，如数字或日期升序。
- **Comparator** 是外部定义比较器，可为同一个类提供不同的排序逻辑。若源码不可更改或需要自定义多种排序，则使用 Comparator。

## Q4: 你在开发中一般怎么选择使用 Comparable 还是 Comparator？
**A4:**
- 如果类本身有唯一且自然的排序需求，比如时间、ID 值升序，可在类里实现 Comparable；如果要对同一类进行多种不同排序，就定义多个 Comparator。有时为了简化开发，直接写成 Comparator 多样化处理，也是一种实践方式。

## Q5: 说说 Java 中常见注解类型，以及为什么注解可以在运行时生效？
**A5:**
- 常用注解有：**@Override**、**@Deprecated**、**@SuppressWarnings** 等。
- 自定义注解可用元注解 **@Retention(RetentionPolicy.RUNTIME)** 使之在运行时保留，再通过反射扫描注解实现对应逻辑。

## Q6: 你在项目里使用注解的场景有哪些？
**A6:**
- 用来做配置，如 **Spring** 框架中的 **@Autowired**、**@Service**、**@Controller** 等，用于自动装配和业务逻辑标识。
- 用来做切面逻辑或 **AOP**，通过注解动态切入安全检查、日志记录、事务管理等处理。
- 用来做参数校验，如 **@NotNull**、**@Size** 等 JSR 规范注解，减少重复模板代码。

## Q7: Java 中哪几种引用？分别有什么作用？
**A7:**
1. **强引用**：默认引用方式，对象不会被回收。
2. **软引用**：在内存不足时才回收，常用于缓存场景。
3. **弱引用**：触发 GC 就被回收，常见于 **WeakHashMap**。
4. **虚引用**：无法直接获取对象引用，通过与 **ReferenceQueue** 联动做高级管理。

## Q8: 生产环境中，SoftReference 和 WeakReference 的使用场景是什么？
**A8:**
- **SoftReference** 最常见用在缓存场景，需要"不足时释放资源"，例如图片缓存或文档缓存。
- **WeakReference** 多用于 Map 结构当 key 不被引用时快速清理，像 **WeakHashMap**；或者对生命周期管理要求更灵活的地方。
