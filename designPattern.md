# 디자인 패턴


* [객체지양 디자인패턴 유튜브](https://www.youtube.com/watch?v=lJES5TQTTWE)
* [싱글톤 패턴](https://woowacourse.github.io/javable/post/2020-11-07-singleton/)
* [팩토리 패턴](https://jdm.kr/blog/180)

* [데코레이터 패턴](https://gmlwjd9405.github.io/2018/07/09/decorator-pattern.html)
```
  # 객체의 결합 을 통해 기능을 동적으로 유연하게 확장 할 수 있게 해주는 패턴
  즉, 기본 기능에 추가할 수 있는 기능의 종류가 많은 경우에 각 추가 기능을 Decorator 클래스로 정의 한 후 필요한 
  Decorator 객체를 조합함으로써 추가 기능의 조합을 설계 하는 방식

  # 상속 상속 구조로 표현해야하는 것을 생성자의 인자로 넘김으로서 간단하게 구현
  public abstract class Root { public abstract void call(); }
  /* 기본 클래스 */
  public class Base extends Root {
    @Override
    public void call() { System.out.println("기본기능"); }
  }
  /* 추가 기능을 구현할 부모 클래스 */
  public abstract class AddFunction extends Root {
    private Root addFunction;
    // '합성(composition) 관계'를 통해 Base 객체에 대한 참조
    public AddFunction(Root addFunction) {
        this.addFunction = addFunction;
    }
    @Override
    public void try() { addFunction.call(); }
  }
  
  /* 추가 기능 예시 클래스 */
  public class Add1 extends AddFunction {
    // 기존 표시 클래스의 설정
    public Add1(Root addFunction) { super(addFunction); }
    @Override
    public void call() {
        super.call(); // 생성자로 들어온 부모 기능을 수행
        addFunction1(); // 추가된 기능을 수행
    }
    // 추가로 부여할 기능 메소드
    private void addFunction1() { System.out.println("추가기능1"); }
  }
  
  public static void main(String[] args) {
      Root root = new Base();
      root.call(); // 기본 기능
      
      Root add1 = new Add1(new Base());
      add1.call(); // 기본 기능 + 추가 기능
      
  }

```
 * [커맨드 패턴](https://gmlwjd9405.github.io/2018/07/07/command-pattern.html)
 * [옵저버 패턴](https://gmlwjd9405.github.io/2018/07/08/observer-pattern.html)
