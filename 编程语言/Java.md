Debug:
修改function调用参数时 至少要改三个地方 **initialization 主函数****signature 函数本身****invoke 调用函数**
基本操作:PQ 声明new Comparator<Type>
使用Built-in Comparator: PriorityQueue<Integer> pq = new PriorityQueue<>(Comparator.reverseOrder());自定义Comparator:lambda 表达式定义public compare()方法
打印一维数组中的内容 for (int[] curr : res) { System.out.println(Arrays.toString(curr));}
String -> int: Integer.parseInt(str) int -> String: “” + intchar -> int: char - ‘0’String -> int: Integer.valueOf(s.substring(i - 1, i + 1));
Comparator implements 
注意观察 helper() function的return 和 main function的return 可能不一致 比如 270. Closest Binary Search Tree Value 

定义空的二维数组 return new int[][]{} 必须要加 new int[] 因为该语句是用来声明类型的
定义二维数组元素int[][] A = {{...},{...}};
substring(start, end) 是左闭右开[start, end) 区间 取得元素个数是end - start个元素, 所以[1,2)只会取出一个元素 string.charAt(1) 
for (Character c : s.**toCharArray()**) {} 
--left / left-- 即使是在递归调用的function之中也会改变外层的left的取值，
打印printf中换行 用 **\n** System.out.printf("s.charAt(%d): %c, \n t.charAt(%d): %c", i, s.charAt(i), i, t.charAt(i));
List 转Array的lambda 写法![img](https://lh6.googleusercontent.com/YR8iy-NeCuKsJigWr2hpxA_oCw_OKbvySUYa3wAlzcfFfZGBPIzuOXifhDhTcPUBYJ0lxWt4ZEI3UyT4jhH7RXxeCAXM_lhPbIQdb6j47GrS2wMYi9r22VFBE4ZYzOvQAJFLpne1)
1 << 3 = 2 的三次方 左移 
细节:记得加声明变量的分号 方法调用的分号 return语句的分号 返回/数据结构中添加的类型: int int[] int[][] TreeNode void boolean 
Tree 计算树的edge 包含root是left + right计算树的node 包含root是left + right + 1Node 和 TreeNode import java.util.Random Random rand = new Random();rand.nextInt(int num) num必须为非负数
变量名 不要随便想当然的起名字什么是尾调用和尾递归?http://www.ruanyifeng.com/blog/2015/04/tail-call.html
queue 和 stack 都是在需要保存多个节点的时候才使用 如果只需要遍历 或修改某一个特定节点 是不需要使用queue 和 stack 的 直接遍历即可
Node是否需要判断!=null 是根据需要来的 如果有node.val 或者 node.next, node.left, node.right等调用语句 那么就是需要判断 当期node != null 
定义一个含有predefined value的 ArrayListList<String> places = Arrays.asList("One", "Two", "Three");res.add(Arrays.asList(nums[i], nums[left], nums[right]));Collections.reverse(level) 可以进行list的翻转 
Merge Interval 中比较器 Lambda 表达式写法int[][] intervals 二维数组Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));
HashMap<String, Boolean> 定义HashMap的时候 需要用包装类进行包装 

对于任何一个递归function 都要问一下 base case 是什么 recursion:

![img](https://lh6.googleusercontent.com/RD_1F8iMk25kM8XzlpDJ39p5lPMjpFnRvHBgy3lYGYppxzT8cRZu2L9wE1vKbauWyN2FBg3_QXSjYcAuqPdS9lEntsvLJ3CHcnDViJRYyxnKqpxT2Vt9RFnqRA1ga-sds2R3DI6M)
![img](https://lh3.googleusercontent.com/pvF9GhEcXhO4u4D-7yMQaSqigO8E53PPAU-sEKdStmZVyhvKEGCf5_Nh0t9APgABx_K1-HLTIyLtwWW4mn0YoIK_xdZ1VSqsDHHR7V-NluQ_92PLSAOPIy5hZoHvbAQ5w-s6d-XS)为什么尾递归只保留了一个调用记录？
写递归的时候一定要清楚目前的自己是在递归调用的哪一层 不要不同层之间混搭，这样就乱了
什么时候需要写Helper() function ？ 当function 返回的参数 或者 传入的参数 不满足你的要求的时候



如果不存在重复/不需要进行计数的字符 可以用boolean[] 否则要用int[] hash 来进行操作 
Deque peek() peekLast() poll() pollLast() Last是后入栈的 











Generic Class Method The key benefit of generics is to enable errors to be detected at compile time rather than at runtime.A generic class or methods permits you to specify allowable types of objects that the class or method can work with. If you attempt to use an incompatible object, the compiler will detect that error.ComparableComparatorcompare() 方法 左边声明List 右边声明LinkedList 是什么意思？ 和左边和右边都声明LinkedList 有什么区别? LinkedList add() API O(n)操作 因为需要向右边移动元素public void add(int index, E element)Inserts the specified element at the specified position in this list. Shifts the element currently at that position (if any) and any subsequent elements to the right (adds one to their indices). HashSet 底层是HashMap 利用了HashMap的散列函数，存的值是HashMap中的keyHashSet的contais() 方法是调用map.containsKey(O)方法的，containsKey(o)是根据hash函数去做散列的，所以与元素的多少无关，无论是多少元素containsKey(o)的时间复杂度基本上O(1) CLASSPATH概念介绍: java.lang.ClassNotFoundException: 因为当前目录中没有字节码, 只能依靠CLASSPATH环境属性 SET CLASSPATH = \user\auguskong\code 在java程序解释的时候 JVM解释的类都是从当前的目录，默认设置为当前目录加载类, 从当前所在路径加载类 SET CLASSPATH = . （设置为当前路径）增加一个全局PATH: 操作系统提供的路径配置, 定义所有可执行程序的路径CLASSPATH:JRE提供的，用于定义Java程序解释时的类加载路径JVM -> CLASSPATH 定义的路径 -> 加载字节码文件 异常的捕获与处理 认识异常对程序的影响, 导致程序中断执行指令流 出现错误之后,整个的程序不会按照既定程序执行 try { 可能出现异常语句}catch 异常类型 异常对象catch 异常类型 异常对象catch 异常类型 异常对象 finally 不管是否出现异常都要执行 try…catchtry…catch…finally printStackTrace()打印完整的异常信息 1. 在程序运行中才会产生异常,一旦产生呢异常后,自动进行异常类对象的实例化处理2. 如果此时程序没有提供异常处理的情况,就会按照JVM的默认处理方式,中断程序的执行3. 如果存在异常处理,这个异常类的实例化对象将会被try语句进行捕获4. try捕获到异常后与其匹配的catch中的异常进行比较, 不匹配继续匹配后序catch5. 如果没有任何catch匹配成功, 则无法执行6. 最终执行finally语句 如果处理过了,则继续向后执行其它代码，如果没有, 则继续JVM默认的异常处理模式 java.lang.Object    	java.lang.Throwable          	java.lang.Exception                	java.lang.RuntimeException                      	java.lang.ArithmeticExceptionThrowable中两个子类Error: 开发者无法处理Exception: 程序中出现的异常,开发者可以处理 异常产生的时候,会产生异常的实例化对象,所有的异常都可以用Exception来处理,有父类的**转型** **(**再理解) 一个Exception可以捕获所有, 但是范围太大, 实际中是将大范围的放到后面,前面的处理不了到最后再来 throws关键字 定义了一个方法,就应该明确的告诉使用者,这个方法可能会产生何种异常,此时就可以在方法的声明上来进行异常类型的标注 **throws的使用** // 如果产生了异常时, 调用者进行处理 两种情况:1. 调用者直接处理, 必须要使用try catch将可能产生异常的方法包裹起来接上2. 如果调用者继续向上抛出异常,则不需要try catchclass MyMath {    	public static int div(int x, int y) throws Ari… {          	return x / y;    	}} RuntimeException 与 Exception区别: RuntimeException 的异常子类可以不需要强制性处理 java.lang.Object    	java.lang.Throwable          	java.lang.Exception                	java.lang.**RuntimeException**                      	java.lang.ArithmeticException **throw的使用**异常对象不是由系统生成的,而是由自己定义的手工进行异常类的抛出, 当前方法进行处理 throw 和 throws的区别throw: 是在代码块中使用throws: 将 **自定义异常类:**两种实现方式:1. 直接继承Exception类 class BoboException extends Exception {    	public BoboException(String msg) {          	super(msg);    	}}2. 继承RuntimeException Iterator 95%的输出 另外5% Enum枚举 Iterator<T> public boolean hasNext() Return true if the iteration has more elementspublic E next() Return the next element取出当前数据default default void remove() remove the last element returned by this iterator UML图UML 统一建模语言 利用图形化形式来实现程序类的关系的描述 抽象类: abstract关键字 + *斜体表示类名称*访问权限:+: public#: protected-: private属性定义 访问权限 属性名称 : 属性类型 例子: + x : int方法定义 访问权限 方法名称() : 返回值例如:+ setDepartmentName() : void+ <<Constructor>> Department() 子类实现接口使用 三角形 和 虚线类的继承使用 三角形 和 实线 可以通过代码直接转化成UML图形 枚举 JDK 1.5之后提出的 主要作用: 定义有限个数对象的一种结构(多例设计), 有枚举之后就不必须使用多例设计了 **enum关键字** 使用enum可以在程序编译时就判断所使用的实例化对象是否存在使用values()来获取所有对象 Enum类是一个抽象类 public abstract class Enum<E extends Enum<E>>extends Objectimplements Comparable<E>, Serializable 方法名称类型作用protected Enum(String name, int ordinal)普通传入名字和序号public final String name()普通获得对象名字public final int ordinal() 普通获得对象序号 定义枚举结构可以定义构造方法,普通方法,属性等 在枚举类中定义其它的结构枚举对象必须写在首行// OKenum Color {	RED, GREEN, BLUE; //实例化对象	private String;} // 报错enum Color {	private String;	RED, GREEN, BLUE; //实例化对象} **单例设计模式** 限定一个类只使用一个实例化对象目的是控制实例化对象  **代理设计模式** 传统代理模式的弊端 基于接口的设计，首先定义核心接口的组成 动态代理模式 首先关注InvocationHandler接口，这个接口规定了代理方法的执行 代理方法调用代理方法调用, 代理主题类中执行的方法最终都是此方法 @proxy 要代理的对象@method 要执行的接口方法名称@args 传递的参数@return 某一个方法的返回值@throws Throwable 方法调用时出现的错误继续向上抛出 public Object invoke(Object proxy, Method method, Object[] args) throws Throwable;
  数字签名数字证书 数字签名是 加密信息的摘要Hash值数字证书是发送方的公钥使用认证机构的私钥进行加密后生成的一个Hash值？ 如何保证数字证书不是伪造的？ 证书如何保证有效性？

需要复习的点:
Java Lambda 表达式Comparator 写法Python 和 Java 的异同点
TreeMap + Red-Black Tree需要了解 Bloomberg 马拉松问题 
(Entry e : map.EntrySet()) {	e.getKey()	e.getValue()}
图的题目一定要先想清楚 Node 和 Edge怎么找,是什么 
字符串的value比较需要用equals() 方法, 直接用 == 和 != 是判断引用是否相同 
Comparator:
Comparator.comparing((int[] p) -> p[0]).thenComparing((int[] p) -> p[1])intervals.sort((o1, o2) -> o1.start - o2.start); 

Java API: 

用例: str = str.trim();public String trim()Returns a string whose value is this string, with any leading and trailing whitespace removed.
用例: str.startsWith(pre);public boolean startsWith(String prefix)Tests if this string starts with the specified prefix.Return true if the character sequence represented by the argument is a prefix of the character sequence represented by this string; false otherwise

英语表达截图:![img](https://lh5.googleusercontent.com/4qChPWqvvmI3nC7tO9BrY69f8qjMuZJAIDHw95vrJxgLF782E8kGAj6fT0-s5B_Mc0bGt_AWWAEZ9k1-843A64_cifV7ZKb9fDSMZ20h_jroLm61tICI68MqngL5jvxzX_Y80Acl)![img](https://lh5.googleusercontent.com/bmKxOyQcwFli1wmOvqy9U-A7asq60PXHaYLoQMFaF9sJdTwPH7IQR5oUUXOyGZYZkOD1EftQRANjv7g1gOwHRxfq6LfKA4a6Xs4QUdm7h_etjimW7KVyiKflULwFwkmd3x-N00_g)![img](https://lh3.googleusercontent.com/11jxmsnlp4uSCrj0vck-_X1y6JxCxPROy0HGsFFpcKcWCfQ_c1MggcA7CqFTWWxmAIvagIzmHjXrOG_I8FNxjTuUJ5h4wlGYF9Sphk18KjLnIZ8uoMAWfOgbI_qKFtgpy5B8lVRM)![img](https://lh4.googleusercontent.com/693yG97PCAt-dMUQDcBtTQft78LYmGCiW7D4kKWxfA1ii2YSy7N9mVdogvArZNauD_NBP85-Jn1vgajBj0wK3phG7oYO_c3ivthfxxE4axtRl63uXnaMVcnH9doGJ1nhTdXOFhDZ)
ampersand & 