# **Chapter6. 흐름 제어**

## 6.1 조건문

### 6.1.1 If 구문

### 6.1.2 switch 구문

다른 언어와 비교했을 때 많이 달라진 문법 중 하나입니다. switch 구문도 소괄호(( ))를 생략할 수 있습니다. 단, break 키워드 사용은 선택 사항입니다. 즉 case 내부의 코드를 모두 실행하면 break 없이도 구문이 종료된다는 뜻입니다. 이 방식은 예상치 못한 실수를 줄이는데 큰 도움이 됩니다. 대신 다른 문법에서 break 없이 case를 연속 실행하던 트릭을 사용하지 못하게 됩니다. case를 연속 실행하기 위해선 fallthrough 키워드를 사용합니다.

- fallthrough: case 바로 아래의 구문을 연속 실행한다.

```swift
let number = 5 // Float, Double도 가능

switch number {
case 0:
    print("Value == zero")
case 1...10:
    print("Value == 1~10")
    fallthrough
case Int.min..<0, 101..<Int.max:
    print("Value < 0 or Value > 100")
    break
default:
    print("10 < Value <= 100")
}

// 결과
// Value == 1~10
// Value < 0 or Value > 100
```

- 숫자 표현 외에도 문자, 문자열, 열거형, 튜플, 범위, 패턴이 적용된 타입도 가능합니다.
- 여러개의 case를 실행하려면 fallthrough 키워드를 쓰거나 case 옆에 나열하면 됩니다.

```swift
let str = "Antony"

switch str {
case "yagom":
    print("He is yagom")
case "Raven":
    print("He is Raven")
case "Antony", "Joker", "Nova":
    print("He or She is \(str)")
default:
    print("\(str) said 'I don't know whe you are'")
}
```

- 튜플을 활용할 수 있습니다.
- 와일드카드 식별자를 사용할 수 있으며 무시된 값을 let으로 받을 수도 있습니다.

```swift
typealias NameAge = (name: String, age: Int)

let tupleValue: NameAge = ("yagom", 99)

switch tupleValue {
case ("yagom", 50):
    print("정확히 맞췄습니다.")
case ("yagom", let age):  // let을 붙여서 값 바인딩을 한다.
    print("이름만 맞췄습니다. 나이는 \(age) 입니다. ")
case (_, 99):  // 와일드 카드로 모든 값 받는다.
    print("나이만 맞췄습니다. 이름은 \(tupleValue.name) 입니다. ")
default:
    print("누구세요?")
}
```

- where 로 case의 조건을 확장할 수 있습니다.

```swift
let position = "사원"
let year = 1
let isIntern = false

switch position {
case "사원" where isIntern == true:
    print("인턴입니다.")
case "사원" where year < 2 && isIntern == false:
    print("신입사원입니다.")
case "사원" where year > 5:
    print("연식이 좀 된 사원입니다.")
case "사원":
    print("사원입니다.")
case "대리":
    print("대리입니다.")
default:
    print("사장입니까?")
}
```

- 열거형을 입력 값으로 받는 switch 구문입니다.
- 모든 case에 대해 대응하는 값을 구현한다면 default를 안붙여도 됩니다.
- 와일드카드(_)를 활용하면 default를 대신할 수도 있습니다.

```swift
enum School {
    case primary, elementary, middle, high, college, university, graduate
}

let education = School.university

switch education {
case .primary:
    print("최종학력은 유치원입니다.")
case .elementary:
    print("최종학력은 초등학교입니다.")
case .middle:
    print("최종학력은 중학교입니다.")
case .high:
    print("최종학력은 고등학교입니다.")
case .college, .university:
    print("최종학력은 대학교입니다.")
case .graduate:
    print("최종학력은 대학원입니다.")
}
```

- 와일드카드는 문법적으로 오류는 없지만 논리적 오류가 발생할 수 있는 여지가 있기 때문에 unknown 속성을 사용할 수 있다.
- 이렇게되면 Switch mush be exhaustive 에러가 발생하게 된다. 이러한 경고를 통해 해당 switch 구문이 모든 case에 대응하지 않는다는 사실을 다시 상기할 수 있습니다. unknown 속성을 부여한 case는 switch 구문의 가장 마지막 case로 작성해야 합니다. 또한 unknown은 case _ 혹은 default case 앞에만 붙일 수 있습니다.

```swift
enum Menu {
  case chicken
  case pizza
  case hamburger
}

let lunchMenu: Menu = .chicken

switch lunchMenu {
case .chicken:
  print("반반 무많이")
case .pizza:
  print("핫소스 많이 주세요")
@unknown case _:
  print("오늘 메뉴가 뭐죠?")
}
```

## 6.2 반복문

### 6.1.1 for-in 구문

### 6.1.2 while 구문

### 6.1.3 repeat-while 구문

- 다른 언어의 do-whlie과슷 비다하슷

```swift
var names: [String] = ["John", "Jenny", "Joe", "yagom"]

repeat {
  print("Good bye \(names.removeFirst())")
} while names.isEmpty == false
```

### 6.3 구문 이름표
