# Springboot启动类注解
## 有三个重要的注解
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan

## 一、@SpringBootConfiguration
这个注解是springboot的配置类，其作用和@configuration注解是基本上是一样的
```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
@Indexed
public @interface SpringBootConfiguration {
    @AliasFor(
        annotation = Configuration.class
    )
    boolean proxyBeanMethods() default true;
}

```
可以看到其实就是直接对configuration注解进行了一层套娃式的封装
当我们在项目中使用了 @Indexed 之后，编译打包的时候会在项目中自动生成METAINT/spring.components文件。根据该文件进行扫描注入，可以提高效率，相当于为为扫描的类创建了索引文件，只需要一次io就能完成全部类的扫描。
当Spring应用上下文执行ComponentScan扫描时，META-INT/spring.components将会被CandidateComponentsIndexLoader 读取并加载，转换为CandidateComponentsIndex对象，这样的话@ComponentScan不在扫描指定的package，而是读取CandidateComponentsIndex对象，从而达到提升性能的目的。

简单点说,使用了@Indexed注解后,原来@ComponentScan可能需要扫描非常多的类,现在只需要在启动后对spring.components进行一次io,将类路径写入文件,后续将只需要读取文件即可获得所有类路径

proxyBeanMethods属性是是否为被注解的类修饰的属性每次都去ioc容器里获取它的代理类，默认为true开启，设置为false关闭后，每次获取这个类的实例会创建一个新的对象且不由IOC容器进行管理

## 二、@EnableAutoConfiguration注解
这个是springboot开启自动配置的核心所在

```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import({AutoConfigurationImportSelector.class})
```

@Import,当注入的类实现了ImportSelector接口,就不会将该类型注入到容器中,而是会注入selectImports方法返回的信息对应的对象(动态使用)