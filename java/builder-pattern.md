# 다양한 디자인 패턴에 대해 공부하자(자바)

## Builder Pattern 
### 개요
기존에 VO(Value Object)들을 생성할 때 아래와 같은 코드르 사용했었다.
'''
// ExampleVO.java
public class ExampleVO
{
  private int number = 0;
  public ExampleVO(int n)
  {
    this.number = n;
  }
}

// Main.java
public class Main
{
  public static void main(String[] args){
    ExampleVO vo = new ExampleVO(55);
  }
}
'''

위 코드르 보면 별로 문제가 될 사항이 보이지 않는다.
아래와 같이 속성 값이 여러개인 경우를 한번 보자
'''
// ExampleMultipleAttributeVO.java
public class ExampleMultipleAttributeVO
{
  private int number = 0;
  private String title = null;
  public ExampleMultipleAttributeVO(int n, String t)
  {
    this.number = n;
    this.title = t;
  }
}

// Main.java
public class Main
{
  public static void main(String[] args){
    ExampleMultipleAttributeVO vo = new ExampleMultipleAttributeVO(10,"example title");
  }
}
'''

위 경우 처럼 속성 값이 여러개인 경우에는 생성자의 함수 순서를 고정으로 해야하고 무조건 Argument의 값을 설정해줘야만 한다.
**Java의 경우엔 Argument의 초기 값 설정이 불가능**

이를 해결하기 위해서 **Builder** 패턴이라는 개념이 등장하게 되었다.
위 경우를 빌더 패턴을 적용해 보았다.

'''
// ExampleMultipleAttributeVO.java
public class ExampleMultipleAttributeVO
{
  private int number = 0;
  private String title = null;
  public ExampleMultipleAttributeVO(int n, String t)
  {
    this.number = n;
    this.title = t;
  }
}

// ExampleMultipleAttributeVOBuilder.java
public class ExampleMultipleAttributeVOBuilder
{
  private int number = 0;
  private String title = null;
  public ExampleMultipleAttributeVOBuilder setNumber(int n)
  {
    this.number = n;
    return this;
  }
  public ExampleMultipleAttributeVOBuilder setTitle(String t)
  {
    this.title = t;
    return this;
  }
  public static ExampleMultipleAttributeVO build()
  {
    return new ExampleMultipleAttributeVO(number, title);
  }
}

// Main.java
public class Main
{
  public static void main(String[] args)
  {
    ExampleMultipleAttributeVO vo = ExampleMultipleAttributeVOBuilder().Builder().
                                                                       .setNumber(10)
                                                                       .setTitle("Builder Pattern Awesome !!").build();
  }
}
'''

<p style="color:'#c0c0c0'">뭔가 코드가 늘어난건 기분 탓 인가...?</p>

코드의 량은 거의 2배 정도 늘어났다.. 근데 Main의 저 아름다운 자태를 보면 그정도의 수고로움은 충분히 감내할 수 있을 거 같다.
항상 자바 코드를 작성하며 재사용성을 중요시 생각하는 나의 경우에는 정말 필요한 패턴이라고 생각한다.
