---
title: "@Configuration vs @Component"
excerpt: ""

categorise:
  - Blog
tags:
  - Blog
---

# @Configuration vs @Component

위의 두 어노테이션은 우리가 스프링에서 Bean 을 등록하고자 할 때 사용된다. 둘다 Bean을 등록하는건대 무엇이 다른걸까?

아래 두 코드를 확인해보자

```java


@Configuration
class test {

  @Bean
  public TestBean getTest(){
      return new TestBean();
  }
  
  @Bean
  public TestConsumeBean getTestConsumeBean(){
      return new TestConsumeBean(getTest());
  }
}
```

```java


@Component
class test {

  @Bean
  public TestBean getTest() {
    return new TestBean();
  }

  @Bean
  public TestConsumeBean getTestConsumeBean() {
    return new TestConsumeBean(getTest());
  }
}
```

위의 두 코드는 어노테이션만 다르고 하는 일은 같은 코드이다. 두 코드는 같아 보이지만 내부에서는 엄연히 다르게 값을 전달해준다.<br>
@Configuration 의 코드는 TestConsumeBean객체를 만들 때 getTest()을 이용하여 기존에 @Bean으로 등록된 TestBean을 가지고 오게도지만
@Component는 그렇지 않다. @Component에서는 getTest()을 사용할때 @Bean에 등록된 객체를 반환해 주는게 아니라 getTest() 메소드를 사용하여 직접 객체를 만들어서 반환해 주게 된다.
즉 TestBean이 @Component 클래스 안에서 싱글톤이 유지 되지 않습니다.