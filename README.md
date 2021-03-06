# JAVA_DESIGN_PATTERNS
Java 设计模式的讲解库，主要适用于学习Java的设计模式
# 1.模板模式的使用方法：
#抽象计算机类：
package template;
/**
 * AbstractComputer
 * @author lidong
 * @2016-02-26
 */
public abstract class AbstractComputer {

	public void powerOn() {
		System.out.println("打开电源");
	}

	public void checkHardware() {
		System.out.println("检查硬件");
	}

	public void loadOS() {
		System.out.println("加入操作系统");
	}

	public void login() {
		System.out.println("小白的计算机无验证，直接进入系统");
	}
	
	public  final void startUp(){
		System.out.println("=====开机==start======");
		powerOn();
		checkHardware();
		loadOS();
		login();
		System.out.println("=====关机==stop======");
	}
}
#实现类
package template;
/**
 * 程序员的计算机
 * @author lidong
 * @2016-02-26
 */
public class CoderComputer extends AbstractComputer {
	
	@Override
	public void login() {
		super.login();
		System.out.println("程序员只需要进行用户和密码的验证就可以了");
	}

}
package template;
/**
 * 航天员的计算机
 * @author lidong
 * @2016-02-26
 */
public class MilitaryComputer  extends AbstractComputer{
    
	@Override
	public void checkHardware() {
		super.checkHardware();
		System.out.println("检查硬件防火墙");
	}
	
	@Override
	public void login() {
		super.login();
		System.out.println("进行指纹识别");
	}
	
}
测试类
package template;

/**
 * 测试方案
 * @author Administrator
 *
 */
public class Test {

	public static void main(String[] args) {
       AbstractComputer comp = new CoderComputer();
       comp.startUp();
       
       comp = new MilitaryComputer();
       comp.startUp();
	}

}


#2.单例模式的使用场景
确保某一个类中只有一个实例，而且自行实例化并且向整个系统提供一个实例。
singleton包下的Singleton是懒汉式单例，Singleton双检查单例，Singleton2饿汉式单例
单例模式的使用场景：
确保某个类有且只有一个实例。避免产生多个对象消耗过多的资源，或者某种类型的对象只应该有且既有一个。
例如创建一个对象需要消耗资源过多，如要访问IO和数据库资源、网络资源，这事就要考虑使用单例
单例模式的关键点：
(1)构造方法私有化，一般为private
(2).通过一个今天方法返回单例对象。
(3)确保单例类对象只有一个，尤其是在多线程的情况下。
(4)确保单例类对象在反序列化时，不重新构建对象。


#3.Builder设计模式
3.1Builder模式的定义
将一个复杂的对象的构建与他的表示分离，使的同样的构建过程可以构建不同的表示。
3.2Builder模式的使用场景
(1)相同的方法，不同的执行顺序，产生不同的事件结果。
(2)多个部件都可以装配到一个对象中，但是产生的运行结果又不相同。
(3)产品类非常复杂，或者产品类中调用顺序不同产生不同的作用，这时候使用建造者模式非常是适合。
(4)当初始化一个复杂的对象，如好多参数，且很多参数都具有默认值。
3.3Builder模式的UML图
Product产品类---产品的抽象
Builder--抽象的Builder，规范产品的组件，一般是由子类实现具体的组件过程。
ConcreateBuilder --具体的Builder类
Director--统一的组件过程。

builder包下Builder。
