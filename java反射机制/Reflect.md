# 一.JAVA的反射机制

## 1.Java反射机制的概念

Java反射就是可以动态的通过一个已知名的class，获取该class的属性和方法等的一切信息。（Java反射概念）Java反射是Java被视为动态（或准动态）语言的一个关键性质。这个机制允许程序在运行时透过Reflection APIs取得任何一个已知名称的class的内部信息，包括其modifiers（诸如public, static 等）、superclass（例如Object）、实现之interfaces（例如Cloneable），也包括fields和methods的所有信息，并可于运行时改变fields内容或唤起methods。

==Java可以加载一个运行时才得知名称的class，获得其完整结构。==

## 2、掌握Class对象的获取和它常见方法的使用

* getName()  一个Class对象描述了一个特定类的特定属性，而这个方法就是返回String形式的该类的简要描述

  ```java
  	Class student1 = Class.forName("com.oak.bean.Student");
  		String name = student1.getName();
  		System.out.println("类名："+name);
      //类名：com.oak.bean.Student
  ```

- newInstance()  该方法可以根据某个Class对象产生其对应类的实例。需要强调的是，它调用的是此类的默认构造方法

  ```java
  Student student = (Student) student1.newInstance();
  		student.setAge(18.0);
  		System.out.println("年龄"+student.getAge());
  //年龄18.0
  ```

* getClassLoader()      返回该Class对象对应的类的类加载器。

  ```java
  Class student1 = Class.forName("com.oak.bean.Student");
  		System.out.println("ClassLoader:"+student1.getClassLoader()); 
  //ClassLoader:sun.misc.Launcher$AppClassLoader@73d16e93
  ```

- getSuperClass()         返回某子类所对应的直接父类所对应的Class对象

  ```java
  Class student1 = Class.forName("com.oak.bean.Student");
  		System.out.println("Superclass:"+student1.getSuperclass()); 
  //Superclass:class java.lang.Object
  ```

* isArray()                      判定此Class对象所对应的是否是一个数组对象。

  ```java
  	Class student1 = Class.forName("com.oak.bean.Student");
  		System.out.println("Superclass:"+student1.isArray()); 
  //Superclass:false
  ```


## 3、掌握Java反射机制的应用

###  1. 得出某个类中所有字段（Fields）的有关信息

public Field getField(String name)  

返回一个 Field 对象，它反映此 Class 对象所表示的类或接口的指定==公共成员==字段

```java
Class student1 = Class.forName("com.oak.bean.Student");
		System.out.println(student1.getField("name"));
// public java.lang.String com.oak.bean.Student.name
```

public Field[] getFields()     它反映此 Class 对象所表示的类或接口的所有==公共成员==字段（数组）

```java
Class student1 = Class.forName("com.oak.bean.Student");
		System.out.println(student1.getFields().length);
// 2
```



public Field getDeclaredField(String name)

返回一个 Field 对象，该对象反映此 Class 对象所表示的类或接口的指定已声明字段(public  ==private== protected)

```java
Class student1 = Class.forName("com.oak.bean.Student");
		System.out.println(student1.getDeclaredField("name"));
//private java.lang.String com.oak.bean.Student.name
```



public Field[] getDeclaredFields()

返回 Field 对象的一个数组，这些对象反映此 Class 对象所表示的类或接口所声明的所有字段

 ```java
Class student1 = Class.forName("com.oak.bean.Student");
		Field[] fs2 = student1.getDeclaredFields();
		int i = 1;
	    for(Field fs:fs2){
	    	System.out.println("属性"+i+":"+fs.getName());
	    	System.out.println("类型名"+i+":"+fs.getType().getName());
	    	i++;
	    }
//	    属性1:id
//	    类型名1:int
//	    属性2:name
//	    类型名2:java.lang.String
//	    属性3:age
//	    类型名3:java.lang.Double
 ```



getFields和getDeclaredFields区别：

getFields返回的是申明为public的属性，包括父类中定义，

getDeclaredFields返回的是指定类定义的所有定义的属性，不包括父类的。

### 2. 得出某个类中所有方法(Methods)的有关信息

public Method  getMethod(String name,Class<?>... parameterTypes)	

返回一个 Method 对象，它反映此 Class 对象所表示的类或接口的指定==公共成员方法

```java
	Class student1 = Class.forName("com.oak.bean.Student");
	// method null
	Method m1 = student1.getMethod("getName", null); 
	System.out.println("method1 = " + m1.toString());  
	// method Integer     
	Class[] cArg = new Class[1]   ;
			cArg[0] =Double.class;     
	Method m2 = student1.getMethod("setAge", cArg);
	System.out.println("method2 = " + m2.toString());  
// method1 = public java.lang.String com.oak.bean.Student.getName()
// method2 = public void com.oak.bean.Student.setAge(java.lang.Double)
```
public Method[] getMethods()	

返回一个包含某些 Method 对象的数组，这些对象反映此 Class 对象所表示的类或接口（包括那些由该类或接口声明的以及从超类和超接口继承的那些的类或接口）的公共方法

```java
	Class student1 = Class.forName("com.oak.bean.Student");
		Method[] students = student1.getMethods();
		int i=0;
		for(Method student:students){
			System.out.println("第"+i+"个方法是："+student.getName());
			i++;
		}
//		第0个方法是：getName
//		第1个方法是：getId
//		第2个方法是：setName
//		第3个方法是：setId
//		第4个方法是：setAge
//		第5个方法是：getAge
//		第6个方法是：wait
//		第7个方法是：wait
//		第8个方法是：wait
//		第9个方法是：equals
//		第10个方法是：toString
//		第11个方法是：hashCode
//		第12个方法是：getClass
//		第13个方法是：notify
//		第14个方法是：notifyAll
```



public Method getDeclaredMethod(Stringname,Class<?>... parameterTypes)

返回一个 Method 对象，该对象反映此 Class 对象所表示的类或接口的指定已声明方法

```java
	Class student1 = Class.forName("com.oak.bean.Student");
		// method null
		Method m1 = student1.getDeclaredMethod("getName", null); 
		System.out.println("method1 = " + m1.toString());  
		// method Integer     
		Class[] cArg = new Class[1]   ;
				cArg[0] =Double.class;     
		Method m2 = student1.getDeclaredMethod("setAge", cArg);
		System.out.println("method2 = " + m2.toString());  
//		method1 = public java.lang.String com.oak.bean.Student.getName()
//		method2 = public void com.oak.bean.Student.setAge(java.lang.Double)
```

public Method[] getDeclaredMethods()	 返回 Method 对象的一个数组，这些对象反映此 Class 对象表示的类或接口声明的所有方法，包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法

```java
	Class student1 = Class.forName("com.oak.bean.Student");
		Method[] students = student1.getDeclaredMethods();
		int i=0;
		for(Method student:students){
			System.out.println("第"+i+"个方法是："+student.getName());
			i++;
		}
//		第0个方法是：getName
//		第1个方法是：getId
//		第2个方法是：setName
//		第3个方法是：setId
//		第4个方法是：getAge
//		第5个方法是：say
//		第6个方法是：setAge
```



### 3. 运行一个类中的某个方法

invoke(obj, args)

**该方法至少有一个参数**

第一个参数为要执行的方法所属的某个类的对象且是Object类型

第二个参数可以是对象，也可以是值（比如string int类型的值等）

 用反射解释spring的set注入

```java
public static void main(String[] args) throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException {
		// TODO Auto-generated method stub
		//加载类(根据地址)
		Class c = Class.forName("com.oak.bean.Student");				
		//实例化对象
		Object obj = c.newInstance();
		//获取类中所有属性
		Field[] fs = c.getDeclaredFields();
		Method[] ms = c.getDeclaredMethods();
		for(Field f:fs){
			String fname = f.getName();
			System.out.println("所有属性名："+fname);
			for(Method m:ms){
				String mname = m.getName();
				System.out.println("方法名："+mname);
				//判断set方法为哪个属性的
				//截取set后面的字符串和属性名匹配 setAge age
				String sub = mname.substring(3).toLowerCase();
				System.out.println("sub = "+sub);
				if(mname.startsWith("set")&& fname.toLowerCase().equals(sub)){
					String tname = f.getType().getName();
					System.out.println("tname = "+tname);
					if("java.lang.String".equals(tname)){
						//执行该对象的set方法进行赋值
						m.invoke(obj, "我是黑客，我很厉害");
					}
				}
			}

		}
		
		//取值
		for(Field f:fs){
			String fname = f.getName();
			System.out.println("所有属性名："+fname);
			for(Method m:ms){
				String mname = m.getName();
				System.out.println("方法名："+mname);
				//判断set方法为哪个属性的
				//截取set后面的字符串和属性名匹配 setAge age
				String sub = mname.substring(3).toLowerCase();
				System.out.println("sub = "+sub);
				if(mname.startsWith("get")&& fname.toLowerCase().equals(sub)){
					String tname = f.getType().getName();
					System.out.println("tname = "+tname);
					if("java.lang.String".equals(tname)){
						//执行该对象的get方法进行取值
						//m.invoke(obj);
						System.out.println("取值："+m.invoke(obj));
					}
				}
			}
		}	
	}
所有属性名：id
方法名：getName
sub = name
方法名：getId
sub = id
方法名：setName
sub = name
方法名：setAge
sub = age
方法名：say
sub = 
方法名：setId
sub = id
tname = int
方法名：getAge
sub = age
所有属性名：name
方法名：getName
sub = name
方法名：getId
sub = id
方法名：setName
sub = name
tname = java.lang.String
方法名：setAge
sub = age
方法名：say
sub = 
方法名：setId
sub = id
方法名：getAge
sub = age
所有属性名：age
方法名：getName
sub = name
方法名：getId
sub = id
方法名：setName
sub = name
方法名：setAge
sub = age
tname = java.lang.Double
方法名：say
sub = 
方法名：setId
sub = id
方法名：getAge
sub = age
所有属性名：id
方法名：getName
sub = name
方法名：getId
sub = id
tname = int
方法名：setName
sub = name
方法名：setAge
sub = age
方法名：say
sub = 
方法名：setId
sub = id
方法名：getAge
sub = age
所有属性名：name
方法名：getName
sub = name
tname = java.lang.String
取值：我是黑客，我很厉害
方法名：getId
sub = id
方法名：setName
sub = name
方法名：setAge
sub = age
方法名：say
sub = 
方法名：setId
sub = id
方法名：getAge
sub = age
所有属性名：age
方法名：getName
sub = name
方法名：getId
sub = id
方法名：setName
sub = name
方法名：setAge
sub = age
方法名：say
sub = 
方法名：setId
sub = id
方法名：getAge
sub = age
tname = java.lang.Double
```



 

### 4.得出某个类的构造方法的信息

获取某个类的构造方法            Constructor[] cons=stuClass.getDeclaredConstructors();



构造方法的前缀修饰符             Modifier.toString(con.getModifiers())

构造方法的名字                         con.getName()

构造方法的参数集                     Class[]   parameterTypes=con.getParameterTypes(); 

用反射解释Spring构造器注入

```java
	public static void main(String[] args) throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException, NoSuchMethodException, SecurityException {
		// TODO Auto-generated method stub
		//加载类(根据地址)
		Class c = Class.forName("com.oak.bean.Student");	
		//获取所有构造器
		Constructor[] cons = c.getDeclaredConstructors();
		System.out.println("构造方法有"+cons.length+"个");
		int i =1;
		for(Constructor con: cons){
			System.out.println("第"+i+"个构造方法："+con.getName());
			//获取构造方法的参数集
			Class[] parameterTypes = con.getParameterTypes();
			int j=1;
			for(Class cla :parameterTypes ){
				System.out.println("第"+i+"个构造方法的第"+j+"个参数为："+cla.getName());
				j++;
			}
			i++;
		}
		//获取指定参数类型的构造方法
		Constructor<?> constructor = c.getConstructor(int.class,String.class,Double.class);
		//实例化，并赋值
		Object obj = constructor.newInstance(1,"Old Wang",28.0);
		System.out.println("Student为："+obj);
	}

//构造方法有2个
//第1个构造方法：com.oak.bean.Student
//第2个构造方法：com.oak.bean.Student
//第2个构造方法的第1个参数为：int
//第2个构造方法的第2个参数为：java.lang.String
//第2个构造方法的第3个参数为：java.lang.Double
//Student为：id=1, name=Old Wang, age=28.0
```



#  二.反射机制的应用

spring内部最核心的就是IOC， 

IOC作用：控制权由对象本身转向容器，由容器根据配置文件去创建实例并创建各个实例之间的依赖关系（Spring根据这些配置，内部通过反射去动态的组装对象）

动态注入，让一个对象的创建不用new了，可以自动的产生，这其实就是利用java里的反射原理.

反射其实就是在运行时动态的去创建、调用对象，Spring就是在运行时，依赖Spring的配置文件来动态的创建对象，和调用对象里的方法的 。  

==Spring的目的：就是让对象与对象（模块与模块）之间的关系没有通过代码来关联，都是通过配置说明管理的（Spring根据这些配置内部通过反射区动态组装对象）==

==spring的一切都是反射==



 



