---
title: Stateful Widget
categories: Flutter
date: 2020-08-14
---



# Stateful Widget

Stateful Widget은 상태를 가지는 위젯이다. - 사용자의 입력을 받음.

## 생명주기

1. `Stateful Widget Construtor` 호출
2. `CreateState()` : State 생성
3. `Build()` : Rendering
4. Stateful Widget의 `constructor`실행 될 때, Stateless Widget의 `Build()` Rendering

---

5. 사용자의 입력 발생
6. Stateful Widget의 `SetState()` 호출
7. State의 변화 발생
   1. `initState()` : 위젯 생성시 최초로 호출 : 한번만 호출되므로 초기화에 주로 사용
   2. `didChangeDependecies()` : `initState()` 다음에 호출 : 위젯이 의존하는 데이터의 객체가 호출될 때마다 호출
   3. `build()` : 반드시 `Widget` 반환해야 하고, 자주 호출
   4. `setState()` : 개발자로부터 자주 호출 : `build()`에서 계속되는 액션을 수행함. 프레임워크에 "데이터가 변경되었음" 알릴 때 사용함
   5. `dispose()` : 객체가 영구적으로 제거
8. 4, 5, 6 과정 실행
9. Stateful의 `didUpdatewidget)` 호출
10. Stateful의 `build()` 호출
11. 다시 4, 5, 6 과정 실행



## SFW 사용법 및 차이점 - [꿈꾸는 시스템 디자이너 블로그](https://here4you.tistory.com/220)

Stateful Widget을 상속하는 위젯 클래스 + State를 상속하는 상태 클래스로 구성된다.

: 대부분의 경우 위젯 클래스는 상태 클래스를 생성시키는 기능만 하는 경우가 많다.

### `setState()`

단순히 Stateful Widget으로 구현한다고 해서, 참조하는 값(속성)의 변화가 그대로 반영되지는 않는다. UI는 자신이 참조하는 `_count`의 값이 변경됨을 알 수 없다.

위젯에 반영하기 위해서 이용하는 메소드가 `setState()`다.

```dart
FloatingActionButton(
  heroTag:null,
	child : Icon(Icons.remove),
	onPressed: () {
    setState( () {
      _count--;
    });
    print("value of _count = $_count");
  }),
```

`_count`의 값을 `setState()`메서드로 감싼 후 변경함.

`setState()`메서드에서 변경된 상태 값을 플랫폼에 전달 - `build()`메서드가 호출된다.

> 위 코드에서는 필드인 _count 변수가 이 화면구성의 상태(State)가 된다. 그리고 이 필드는 Text 위젯에서 참조하고 있다. 각 버튼이 클릭될 때 setState 메서드 내부에서 상태 값인 _count의 값을 변경하면, 변경과 동시에 변경 사실이 플랫폼으로 전달되어 build 메서드가 다시 호출되게 되고 Text 위젯은 참조하고 있는 _count의 최신 값을 화면에 출력하게 되는 것이다.

### 정리

- SFW은 화면의 구성이 상태 변화에 따라 재구성되어야 할 때 사용된다.
- SFW의 상태 변경은 `setStat() `메서드를 이용해서 변경해야 한다.
- 플랫폼은 `setState()`메서드가 호출될 때마다 `build()`메서드를 호출하여 화면을 다시 그린다.

---

# Stateless Widget

Stateless Widget : 변화가 필요 없는 화면을 구성할 때 사용함.

상태를 가질 수 없으며, 상태가 없으니, 변화를 인지할 필요도 없다. 따라서 `build()` 는 한번만 호출된다.





