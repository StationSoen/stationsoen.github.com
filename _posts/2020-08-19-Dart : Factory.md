---
title : Dart : Factory
date : 2020-08-19
categories : Flutter
---

## Factory : [참고](https://software-creator.tistory.com/5)

팩토리 생성자는 팩토리 패턴을 쉽게 쓰기 위해 만들어졌음.

### 팩토리 패턴 (JAVA) : [참고](https://jusungpark.tistory.com/14)

> **팩토리 메소드 패턴**
>
> 객체를 생성하기 위한 인터페이스를 정의하는데, 어떤 클래스의 인스턴스를 만들어지는 서브 클래스에서 결정하게 만든다. 즉, 팩토리 메소드 패턴을 이용하면 클래스의 인스턴스를 만드는 일을 서브클래스에게 맡기는 것.
>
> **추상 팩토리 패턴**
>
> 인터페이스를 이용하여 서로 연관된, 또는 의존하는 객체를 구상 클래스를 지정하지 않고도 생성.

`new`를 사용하는 것은 구상 클래스의 인스턴스를 만드는 것임.

```java
Duck duck;
  if(type == picnic) {
    duck = new MallardDuck();
  }
	else if(type == hunting) {
    duck = new DecoyDuck();
  }
else {
  duck = new NormalDuck();
}
```

변경하고 확장해야 할 때, 번거로워짐.

인터페이스에 맞춰서 코딩을 하면 시스템의 여러 변화를 이겨낼 수 있음.

> **다형성 - 인터페이스**
>
> 자바 인터페이스는 추상 메서드(구현부가 없는 메서드)의 모음이다. 따라서 인터페이스를 구현하기로 한 클래스는 인터페이스에 명시되어 있는 **추상 메서드를 모두 구현해야 한다.** 
>
> 상속받은 클래스 또는 인터페이스의 메서드를 재정의하여 서로 다른 행동을 만들 수 있다.  상속은 **IS-A** 관계, 인터페이스는 **CAN-DO** 관계라고 할 수 있다.



---

### 예시 : [참고](https://jdm.kr/blog/180)

```java
package pattern.factory;

public abstract class Robot {
	public abstract String getName();
}
// Robot class는 getName을 가져야 함.

public class SuperRobot extends Robot {
	@Override
	public String getName() {
		return "SuperRobot";
	}
}
// SuperRobot class

public class PowerRobot extends Robot {
	@Override
	public String getName() {
		return "PowerRobot";
	}
}
// PowerRobot class
```

```java
package pattern.factory;

public abstract class RobotFactory {
	abstract Robot createRobot(String name);
}
// RobotFactory는 createRobot을 가져야 함.

public class SuperRobotFactory extends RobotFactory {
	@Override
	Robot createRobot(String name) {
		switch( name ){
			case "super": return new SuperRobot();
			case "power": return new PowerRobot();
		}
		return null;
	}
}
// SuperRobotFactory class
```



> 팩토리 메소드 패턴을 사용하는 이유는 클래스 간의 결합도를 낮추기 위한 것입니다. 결합도라는 것은 **클래스의 변경점이 생겼을 때 얼마나 다른 클래스에도 영향을 주는가**입니다.

메인 코드에서 `new` 명령어를 사용하지 않음으로써, 메인 코드의 안정성을 높이고, 수정 및 확장에 용이하게 된다.

---

```dart
abstract class Robot {

  Robot.create();

  factory Robot(RobotType type) { // 팩토리 생성자
    switch(type) {
      case RobotType.Clean:
        return CleanRobot();
      case RobotType.War:
        return WarRobot();
    }
  }

  String getName();
  String command();
}

enum RobotType{
  Clean,War
}
```

```dart
class CleanRobot extends Robot {

  CleanRobot(): super.create();

  @override
  String getName() {
    return "Clean";
  }

  @override
  String command() {
    print("clean a room");
    return "clean a room";
  }
}

class WarRobot extends Robot {

  WarRobot(): super.create();

  @override
  String getName() {
    return "War";
  }

  @override
  String command() {
    print("declare war");
    return "declare war";
  }
}
```

```dart
Robot r1 = Robot(RobotType.Clean);
r1.command();
Robot r2 = Robot(RobotType.War);
r2.command();
```

