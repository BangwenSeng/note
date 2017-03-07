php面向对象
================================================================================

对象是客观存在的一个实体。
类是对对象抽象的一个描述。

概念：对象，类；

类与对象的关系。
	类的实例化就是一个对象
	$person = new person;
	对象           类
	对对象的抽象描述就是一个类
oop面向对象编程的特点：封装，继承，多态

##1.如何定义一个类

	1.1语法格式；
		[修饰符] class 类名
		{
			成员属性
			成员方法
		}
	1.2 其中成员属性个数：
		修饰符 $变量名 = [默认值];
		如：public $name = "张三";
		注意：成员属性不可以是带运算符的
		表达式，变量，方法或者函数的调用

		常见属性的修饰符：public,protected、private、satatic、var


	1.3 其中成员方法格式：
		[修饰符] function 方法名
		{

		}

##2.构造函数和析构函数

	2.1.构造方法(构造函数)：
		当我们通过New 关键字来创建一个对象时。第一个自动执行的方法称为构造方法。
		方法名 __contruct();
		主要用于初始化对象

	2.2.析构方法：当这个对象被销毁时最后自动
		调用的方法，称为析构方法
		__destruct();目的是释放资源(如关闭连接，文件，数据库，释放资源) 

##3.封装(访问控制)

	1、封装就是就属性私有，并提供公有的seter防止与geter取值方法

		public(公有) protected(受保护)

		private(私有)
					public  		protected  			private
		在本类中      Y               Y                   Y
	 	在子类中      Y               Y                   N 
	  	在类外边      Y               N                   N


## 4.重载

 	1.四个魔术方法：__set() __get() __isset()
 		__unset()

 		__get():当我们之间输出一个对象中非公有属性时会自动调用的方法
 			并将属性名以第一个参数穿进去。

 		__set():当我们之间设置一个对象中的非公有属性时会自动调用的方法，
 			并将属性名以第一个参数，值作为第二个参数穿进去

 		__isset()当对未定义的变量调用isset() 或 empty()时，__isset() 会被调用。
		   //当isset判断一个对象的非公有属性是否存在时，自动调用此方法。
		   public function __isset($param){
			  return isset($this->$param);
		   }
		   
	  	__unset()当对未定义的变量调用unset()时，__unset() 会被调用。
		   //当unset销毁一个对象的非公有属性时，自动调用此方法。
		   public function __unset($param){
			  unset($this->$param);
		   			
----------------------------------------------------------------------------------------
## 5、继承

 	1.继承：extends
 	1. 继承特性
	 *
	 *     a. PHP只支持单继承,只能有一个亲爹
	 *     b. 子类会继承父类所有属性，方法
	 *     c. 一个类可以多个类继承。风流的爸爸可以有多个私生子
	 *     d. 可以多层继承。 A类  => B类  => C类 
	 *         A类会有B类以及C类所有属性，方法.只不过私有的属性，方法不能用。
	 *
 	*
	 * 属性继承特点：
	 *
	 *   1. 子类会覆盖父类同名的属性，但是除了私有属性
	 *   2. 当子类中有与父类同名的属性，子类的属性修饰符只能更加松散或者相等，不能更加严谨
	 *
	 *      松散度： public >  protected > private
	 *      严谨度： private > protected > public

	 	方法继承特点:
	 	  1. 子类与父类同名的方法，修饰符只能更加松散
	 *	  2. 子类会覆盖父类非私有的同名方法

	 	用这个parent::__construct($name, $sex);传递父类的构造方法；



##	6、final 、static
 	1.final关键字：主要用于修饰类和成员方法
 		使用final关键字修饰类，表示这个类不可以有子类

	 *  a. final修改类与方法，不能修饰属性
	 *  b. 被修饰的类，叫做最后的类，这个类不被继承
	 *  c. 被修饰的方法，也是不能被重写
 		使用final 修饰方法，不可以重写

 	2.static关键字:表示静态的意思。用于修饰类的属性和方法
 		static关键字修饰方法称为静态方法

 		可以不New就可以直接使用方法
 			如类名::方法名

 		static关键字修饰属性称为静态属性，可以不用new（实例化）就可以直接访问属性：如 类名::属性名
			 注意：静态属性在实例化后的对象不可以访问； //$对象名->静态属性名

		注意:静态属性是共享的也就是new很多对象也是公用一个属性

			4. 静态属性访问方式：

		      a. 类内部：  self::$属性名
		      b. 类外部：
		      		类名::$属性名

	 	   5. 静态方法的访问方式
		       a. 类内部： self::方法名()

		       b. 类外部: 类名::方法名()

			在静态方法中不能使用$this

########################################################################################

7、其他魔术方法：
-----------------------------------------------------------------
	1. 对象复制clone 克隆一个对象，因为对象属于引用类型，普通的“=”号属于引用赋值，
		所有需要clone来复制一份。
		魔术方法：__clone() 当执行clone克隆时会自动调用的方法。
	
	2. __toString()方法：魔术方法，当我们直接要输出一个对象时，如echo $a,print $a，
		那么会自动调用的方法。
		注意：__toString()方法必须返回一个字串类型的值。


	3. *自动加载类函数__autoload(类名): 
		当new 实例化一个对象时，这个类若不存在，则自动调用此函数，并将类名存入参数
		我可以使用这个实现类的自动加载。

		
##8、 对象序列化(串行化)(webservice  XML)(在对象持久化存储、和传输中使用)
----------------------------------------------------------------------------------------------
	serialize() -- 串行化
	unserialize() -- 反串行化

	php里面的值都可以使用函数serialize()来返回一个包含字节流的字符串来表示。
	unserialize()函数能够重新把字符串变回php原来的值。 
	序列化一个对象将会保存对象的所有变量，但是不会保存对象的方法，只会保存类的名字。

	__sleep 和 __wakeup 
	
		__sleep(): 是执行串行化时自动调用的方法，目的是实现资源类型的属性实关闭操作。
			注意：sleep方法需要返回一个数组，其中数组中的值是串行化时要保留的属性名
			
		__wakeup():是在执行反串行化时自动调用的方法，目的是实现资源属性的打开（sleep方法关闭的资源）

	public function __seep(){
        return array('server', 'username', 'password', 'db');
		//此串行化要保留四个属性
    }

    将json数据解码,json_decoce()第二个参数默认是false,返回对象。

    //将$data数组进行json编码
	$res = json_encode($data);


	
##9、错误处理：
	
		1.错误是在开发阶段遇到的bug

		2.错误分类.

			a.致命错误
			b.语法错误
			c.逻辑错误
		3.错误级别
			notice  可以不管

			warning 一般不管

			error    一定要处理

		4.改变错误级别
			a.error_reporting()函数修改

			b.直接修改php.ini的error_reporting

			//显示所有错误
			error_reporting(E_ALL)

			//屏蔽所有错误
			error_reporting(0);

			//值显示致命错误
			error_reportion(E_ERROR)


		5.异常：在项目运行阶段遇到的bug

	//抛出异常 throw new Exception();


	捕获异常信息

		try{
		
			//写可能抛出异常的代码

		}catch(Exception $e){

			//获取到异常信息
		}

	1.try{}catch(){}特点
		1.异常后的代码不执行,catch区间执行

		2.一个try可以有多个catch,只是有一个catch

		3.如果try区间没有抛出异常，catch区间不执行

	###################
	//多态：不同的对象调用同一个方法，出现的结果不同



## 10、接口和抽象类



 		抽象类定义：
	 *
	 *    abstract class 类名
	 *    {
	 *    	  [方法]
	 *
	 * 		  [属性]
	 * 		  [抽象方法]
	 *    }
	 *
	 * 抽象类的特点
	 	定义：

	abstract class Base
	{

		public static $name = 'jack';

		//定义一个方法，但是这个方法架构师不写。
		abstract public function read();//定义了一个抽象方法

		//抽象类中可以有普通的方法
		public function demo()
		{
			echo 'aa';
		}

		public static function test()
		{
			echo 'test';
		}

	}
	 *   1.  抽象类中可以有普通的方法
	 *   2.  抽象类中可以有抽象方法，也可以没有
	 *   3.  抽象类中可以有静态方法
	 *   4.  抽象类中可以有属性
	 *
	 *   5.  继承了抽象类的子类，必须实现抽象类中的抽象方法 或者将子类也定义成抽象类
	 *
	 *   6.  抽象类不能被实例化，不能new

	  抽象类作用：约束子类必须完成一些功能，必须实现一些方法




	 *  接口:一种特殊的抽象类
	 *
	 *  语法：
	 *
	 *      定义：
	 *
	 *        interface 接口名
	 *        {
	 *        		[类常量]
	 *        		[抽象方法]
	 *        }
	 *
	 *   接口需要注意问题：
	 *     1. 接口中不能有成员属性，可以有常量
	 *     2. 接口中的方法都是抽象方法，并且抽象方法不能加abstract。
	 *     3. 接口不能被extends继承，只能使用implements来实现
	 *     4. 接口中的方法，被子类继承后必须实现或者将子类变成抽象类
	 *     5. 可以多实现接口


		 /*
		 类型约束： 只能对数组(Array)/类/回调函数进行约束
		 */
		

		//研究如何约束类
		class Person
		{
			//约束$obj对象必须是M类的实例
			public function gan(M $obj)
			{

				$obj->jiao();
			}
		}

##11、PDO预处理SQL注入的例子

				/**
		 * 这个例子研究如何使用预处理功能防止SQL注入
		 */

		$dsn = "mysql:host=localhost;dbname=lamp25;charset=utf8";

		$pdo = new PDO($dsn, 'root' ,'123');
		
		//问号占位符?
		$sql = "select * from user_detail where id =1 and phone=?";


		//prepare()方法就是预处理的方法
		$stmtObj = $pdo->prepare($sql);//使用prepare先把SQL模板发送给数据库


		//这个数据是用户提交的
		// $phone = "' or 1=1;#'";
		$phone = "1234567";

		//将用户传递过来的数据绑定到参数
		$stmtObj->bindValue(1, $phone);//1代表将$phone这个参数绑定到第一个?


		//执行预处理语句
		$bool =  $stmtObj->execute();
		var_dump($bool);


		//拿到查询的结果
		$list = $stmtObj->fetchAll();

		echo '<pre>';
		print_r($list);


##12、PDO事务
		 事务处理： 把多条SQL语句，把多个操作看成一个整体。这个整体要们全部执行成功，要么都执行失败。
		 *
		 * 事务处理的目的：为了保证数据一致性、完整性。
		 *
		 * 事务处理只针对：增、删、改(update)。没有查询，对修改表结构也是没有用的。
		 *
		 * 事务需要注意的问题：
		 *   1. mysql是支持事务的，但是只有innodb支持事务
		 * 
		 * 例子：
		 *
		 *     1. 银行转账
		 *
		 *         jack要向mary转账300
		 *
		 *             a. jack的账户减去300
		 *             b. mary的账户加上300
		 *
		 *              如果在jack减钱成功，但是在mary加钱，数据库刚好挂掉了。
		 *
		 *      2.  用户注册的时候
		 *
		 *           需要插入：name/pass/email
		 *
		 *           user表：name/pass
		 *           user_detail表：email
		 *
		 * 与事务有关的mysql语句：
		 *
		 * //开启事务
		 * mysql> begin;
		 *
		 * //事务成功，需要提交
		 * mysql> commit;
		 *
		 * //事务失败,任何一个步骤失败都要回滚
		 * mysql> rollback;
		 *
		 * ===============================
		 * myisam与innodb引擎的区别(面试重点)
		 *   1. 锁机制不一样
		 *
		 *      myisam支持表锁，innodb支持行锁，表锁
		 *
		 *   2. 查询速度不一样
		 *
		 *      一般认为myisam查询速度相对innodb快
		 *
		 *   3. 事务处理不一样
		 *
		 *      innodb支持事务的，myisam不支持事务
		 *
		 *   4. 数据保存方式
		 *
		 *       如果是MyISAM引擎，会在磁盘产生三个文件，分别是.MYD，存放数据，
		 *
		 * .MYI存放索引的，.frm存放表结构。
		 *
		 *       如果是innodb引擎，ibdata1就是存放所有innodb引擎的数据的。
		 *
		 * 	
		 *            
		 *              
		 */
		
		$dsn = "mysql:host=localhost;dbname=lamp25;charset=utf8";

		$pdo = new PDO($dsn, 'root', '123');

		//设置错误级别
		$pdo->setAttribute(3, 2);


		$flag = true;

		//开启事务
		$pdo->beginTransaction();

		//jack给mary 100块钱
		$sql = "update user set money=money-300 where name = 'jack'";

		$row = $pdo->exec($sql);

		if ($row != 1) {

			//$row不等于1，就说明上面那条语句失败，失败就回滚
			$flag = false;
		}


		$sql1 = "update user set money=money+100 where name = 'rose'";

		$row1 = $pdo->exec($sql1);


		if ($row1 != 1) {

			//$row1不等于1，就说明上面那条语句失败，失败就回滚
			$flag = false;
		}


		$sql1 = "update user set money=money+200 where name = 'boss'";

		$row1 = $pdo->exec($sql1);

		if ($row1 != 1) {

			$flag = false;
		}


		if ($flag) {

			echo '成功进行了一次黄色交易<br/>';
			//事务成功
			$pdo->commit();

		} else {

			echo '警察来，交易失败';

			$pdo->rollback();

		}

##13、命名空间namespace
	/**
	 * 命名空间相当于目录，一个DB类发放到Github目录中，
	 * 另外一个DB类放到My目录下。所以就不冲突
	 * 命名空间的作用：是为了避免名字冲突
	 */

	//我们以后经常会去github下载代码放到项目中使用
	
	//定义一个命名空间
	namespace Github;


	/*
		命名空间需要注意的问题：
		1. 不能以数字开头
		2. 命名空间必须在脚本的第一行，命名空间前不能有任何输出


	//命名空间对哪些东西起作用
	//1. 类  2. const定义的常量 3. 函数


	//1. 通过绝对路径(常用)
	new \Github\Home\Cpphp\My\A();

	//2. 取别名的方式
	use Github\Home\Cpphp\My as csdn;

	new csdn\A();

	//3. 直接将Github\Home\Cpphp\My空间的A类导入(常用)
	use \Github\Home\Cpphp\My\A as B;//因为Your空间下就有A类，所以导入A类时，需要取别名