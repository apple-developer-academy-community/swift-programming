# **Chapter4. 데이터 타입 고급**

## 4.1 데이터 타입 안심

스위프트의 특징 중 안정성이 가장 뚜렷하게 나타나는 부분이다. 스위프트는 타입에 굉장히 민감하고 엄격하다. 서로 다른 타입끼리의 데이터 교환은 타입캐스팅을 거쳐야만 한다. 스위프트에서 값 타입의 데이터 교환은 엄밀히 말하면 타입캐스팅이 아닌 새로운 인스턴스를 생성하여 할당하는 것입니다.

### **4.1.1 데이터 타입 안십이란**

스위프트는 데이터 타입을 안심하고 사용할 수 있는 언어입니다. 스위프트는 컴파일 시 타입 확인을 해주며 여러 타입을 섞어 사용할 때 발생할 수 있는 런타임 오류를 피할 수도 있습니다.

### **4.1.2 타입 추론**

스위프트에서는 변수나 상수를 선언할 때 특정 타입을 명시하지 않아도 됩니다.

```swift
var name = "Antony"
print(type(of: name))  // String
```

## 4.2 타입 별칭

스위프트에서 기본으로 제공하는 데이터 타입이든, 사용자가 임의로 만든 데이터 타입이든 이미 존재하는 데이터 타입에 임의로 다른 이름(별칭)을 부여할 수 있습니다.

```swift
typealias MyInt = Int    // MyInt는 Int의 또 다른 이름
typealias YourInt = Int  // YourInt는 Int의 또 다른 이름
```

## 4.3 튜플

튜플은 타입이 따로 지정되어 있지 않은, 프로그래머 마음대로 만드는 타입입니다. ‘**지정된 데이터 묶음**’이라고 표현할 수 있습니다. C 언어를 예로 들자면 원시 구조체의 형태와 가깝습니다. 튜플은 타입 이름이 따로 없으므로 일정 타입의 나열만으로 튜플 타입을 생성해줄 수 있습니다. 튜플에 포함될 데이터의 개수는 자유롭게 정할 수 있습니다.

```swift
// String, Int, Double 타입을 갖는 튜플
var person: (String, Int, Double) = ("Antony", 100, 182.9)

// 인덱스를 통해 값을 빼 올 수 있습니다.
print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2)")

// 인덱스를 통해 값을 할당 가능
person.1 = 90
person.2 = 178.3
```

튜플의 각 요소가 어떤 의미인지 유추하기 어려우므로 튜플의 요소마다 이름을 붙여줄 수 있습니다.

```swift
// String, Int, Double 타입을 갖는 튜플
var person: (name: String, age: Int, height: Double) = ("Antony", 100, 182.9)

// 요소 이름을 통해 값을 빼 올 수 있습니다.
print("이름: \(person.name), 나이: \(person.age), 신장: \(person.height)")

// 요소 이름과 인덱스를 통해 값을 할당 가능
person.age = 90
person.2 = 178.3
```

타입 별칭을 사용하여 조금 더 깔끔하고 안전하게 코드를 작성할 수 있습니다.

```swift
typealias PersonTuple = (name: String, age: Int, height: Double)

let antony: PersonTuple = ("Antony", 100, 178.5)

print("이름: \(antony.name), 나이: \(antony.age), 신장: \(antony.height)")
```

## 4.4 컬렉션형

스위프트는 튜플 외에도 많은 수의 데이터를 묶어서 저장하고 관리할 수 있는 컬렉션 타입을 제공합니다. 배열, 딕셔너리, 세트 등이 있습니다.

### 4.4.1 배열

배열은 같은 타입의 데이터를 일렬로 나열한 후 순서대로 저장하는 형태의 컬렉션 타입입니다.

> 스위프트의 Array는 C언어의 배열처럼 버퍼입니다. 단, C언어처럼 한 번 선언하면 크기가 고정되던 버퍼가 아니라 필요에 따라 자동으로 버퍼의 크기를 조절해주므로 요소의 삽입 및 삭제가 자유롭습니다. 스위프트는 이런 리스트 타입을 Array, 즉 배열이라고 표현합니다. 기존 언어의 배열과는 조금 다른 특성도 있지만 이 책에서도 Array를 배열이라고 표현하겠습니다.
> 

Array<Stirng>과 [String]은 같은 표현입니다.

- 배열 슬라이싱
    
    새로운 배열을 만드는 것이 아니라 기존 배열을 참조하는 형태입니다.
    
    접근 불가능한 요소의 수명을 연장 시킬 수 있으며, 이는 메모리 및 객체 누출(object leakage)로 나타날 수 있습니다. ([https://zeddios.tistory.com/600](https://zeddios.tistory.com/600))
    
    ```swift
    var names = ["a", "b", "c", "d", "e"]
    print(names[1 ... 3])  // ["b", "c", "d"]
    
    names[...2] = ["f", "g", "h"]
    print(names)           // ["f", "g", "h", "d", "e"]
    ```
    

### 4.4.2 딕셔너리

딕셔너리는 요소들이 순서 없이 키와 값의 쌍으로 구성되는 컬렉션 타입입니다. 키는 같은 이름을 중복할 수 없으며 값을 대변하는 유일한 식별자 입니다. 값은 유일하지 않으며 없는 키로 접근하면 nil을 반환합니다. 

키에 해당하는 값을 제거하려면 removeValue(forKey:) 메서드를 사용합니다.

```swift
var numberForName: [String: Int] = [String: Int]()  // 초기화
var numberForName: [String: Int] = [:]  // 초기화
```

### 4.4.3 세트

세트는 같은 타입의 데이터를 순서 없이 하나의 묶음으로 저장하는 형태의 컬렉션 타입입니다. 세트 내의 값은 모두 유일한 값, 즉 중복된 값이 존재하지 않습니다. 

순서가 중요하지 않거나 각 요소가 유일한 값이어야 하는 경우에 사용합니다.

또, 세트의 요소로는 해시 가능한 값(Hashable protocol 준수)이 들어가야 합니다. 

집합 관계를 표현할 때 유용하게 쓸 수 있습니다. 두 세트의 교집합, 합집합 등을 연산하기에 좋습니다. 또한 sorted() 메서드를 통해 정렬된 배열을 반환해줄 수도 있습니다.

```swift
var numberForName: Set<String> = Set<String>()  // 초기화
var numberForName: Set<String> = []  // 초기화

// Set을 쓰고 싶은 경우엔 타입 명시를 해주어야 합니다.
var numbers = [100, 200, 300]  // Array<Int>
```

- 메소드
    - intersection: 교집합
    - symmetricDifference: 여집합의 합(배타적 논리합)
    - union: 합집합
    - subtracting: 차집합
    - isDisjoint: 서로 배타적인지 확인
    - isSubset: 부분집합인지 확인
    - isSuperset: 전체집합인지 확인

### 4.5 열거형

열거형은 연관된 항목들을 묶어서 표현할 수 있는 타입입니다. 열거형은 배열이나 딕셔너리 같은 타입과 다르게 프로그래머가 정의해준 항목 값 외에는 추가/수정이 불가합니다. 그렇기 때문에 딱 정해진 값만 열거형 값에 속할 수 있습니다.

ex) 사용 예

- 제한된 선택지를 주고 싶을 때
- 정해진 값 외에는 입력받고 싶지 않을 때
- 예상된 입력 값이 한정되어 있을 때

스위프트의 열거형은 항목별로 값을 가질 수도, 가지지 않을 수도 있습니다. 예를 들어 C언어는 열거형의 각 항목 값이 정수 타입으로 기본 지정되지만, 스위프트의 열거형은 각 항목이 그 자체로 고유의 값이 될 수 있습니다.

기존의 C언어 등에서 열거형은 주로 정수 타입 값의 별칭 형태로 사용이 되었지만 스위프트의 열거형은 각 열거형이 고유의 타입으로 인정되기 때문에 실수로 버그가 일어날 가능성을 원천 봉쇄할 수 있습니다.

물론 열거형 각 항목이 Raw Value라는 형태로 (정수, 실수, 문자 타입 등의) 실제 값을 가질 수도 있습니다. 또는 Associated Value를 사용하여 다른 언어에서 공용체라고 불리는 값의 묶음도 구현할 수 있습니다.

참고: 스위프트의 옵셔널은 enum으로 구현되어있습니다.

### 4.5.1 기본 열거형

각 항목은 그 자체가 고유의 값입니다.

```swift
enum School {
  case elementary
  case middle
  case high
  case university, graduate
}
```

메서드도 추가할 수 있습니다.

```swift
enum Month {
    case dec, jan, feb
    case mar, apr, may
    case jun, jul, aug
    case sep, oct, nov
    
    func printMessage() {
        switch self {
        case .mar, .apr, .may:
            print("따스한 봄~")
        case .jun, .jul, .aug:
            print("여름 더워요~")
        case .sep, .oct, .nov:
            print("가을은 독서의 계절!")
        case .dec, .jan, .feb:
            print("추운 겨울입니다")
        }
    }
}

Month.mar.printMessage()
```

### 4.5.2 원시 값

열거형의 각 항목은 자체로도 하나의 값이지만 항목의 raw value도 가질 수 있습니다. 즉 특정 타입으로 지정된 값을 가질 수 있다는 뜻입니다.

```swift
enum School: String {
  case elementary = "초등학교"
  case middle = "중학교"
  case high = "고등학교"
}

print(School.high.rawValue)
```

### 4.5.3 연관 값

열거형 내의 case가 자신과 연관된 값을 가질 수 있습니다. 연관된 값은 각 항목 옆에 소괄호로 묶어서 표현할 수 있습니다. 모든 항목이 연관 값을 가질 필요는 없습니다.

```swift
enum MainDish {
    case pasta(taste: String)
    case pizza(dough: String, topping: String)
    case rice
}

enum PastaTaste {
    case cream, tomato
}
var dinner = MainDish.pasta(taste: PastaTaste.tomato)
```

### 4.5.4 항목 순회

열거형에 있는 모든 케이스를 알아야 하는 상황이 생긴다. 그럴 때 CaseIterable 프로토콜을 채택하면 된다. 그러면 열거형에 allCases라는 이름의 타입 프로퍼티를 통해 모든 케이스의 컬렉션을 생성해줍니다.

```swift
enum School: String, CaseIterable {
  case primary = "유치원"
  case elementary = "초등학교"
}

let allCases: [School] = School.allCases // [School.primary, School.elementary]
```

allCases 프로퍼티를 바로 사용할 수 없는 경우가 있는데 열거형의 케이스가 연관 값을 가지고 있는 경우입니다. 이러한 경우에는 직접 allCases 프로퍼티를 구현해서 사용해야 합니다.

### 4.5.5 순환 열거형

순환 열거형은 열거형 항목의 연관 값이 열거형 자신의 값이고자 할 때 사용합니다. 순환 열거형을 명시하고 싶으면 indirect를 붙이면 되며 특정 항목에 한정하고 싶다면 case 앞에, 전체에 적용하고 싶다면 enum 앞에 indirect 키워드를 붙이면 됩니다.

indirect 키워드는 예제 뿐만 아니라, 이진 탐색 트리 등의 순환 알고리즘을 구현할 때 유용하게 사용할 수 있습니다.

```swift
enum ArithmeticExpression {
  case number(Int)
  indirect case addition(ArithmeticExpression, ArithmeticExpression)
  indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}

let five = ArithmeticExpression.number(5)
let nine = ArithmeticExpression.number(9)
let final = ArithmeticExpression.multiplication(five, nine)

func evaluate(_ expression: ArithmeticExpression) -> Int {
  switch expression {
  case .number(let value):
    return value
  case .addition(let left, let right):
    return evaluate(left) + evaluate(right)
  case .multiplication(let left, let right):
    return evaluate(left) * evaluate(right)
  }
}

let result: Int = evaluate(final)
print(result) // 45
```

### 4.5.6 비교 가능한 열거형

Comparable 프로토콜을 준수하는 연관 값만 갖거나 연관 값이 없는 열거형은 Comparable 프로토콜을 채택하면 각 케이스를 비교할 수 있습니다. 앞에 위치한 케이스가 더 작은 값이 됩니다.

```swift
enum Device: Comparable {
    case iPhone(version: String)
    case iPad(version: String)
    case macBook
    case iMac
}

var devices: [Device] = []
devices.append(Device.iMac)
devices.append(Device.iPhone(version: "6.1"))
devices.append(Device.iPhone(version: "14.3"))
devices.append(Device.iPhone(version: "12.2"))
devices.append(Device.iPad(version: "12.2"))
devices.append(Device.macBook)

print(devices)
let sortedDevices = devices.sorted()
print(sortedDevices)
```

![image](https://user-images.githubusercontent.com/57349859/202460733-402b85b9-035a-45ca-9a5c-c9b0146837a8.png)

정렬한 결과, enum에서 앞에 위치한 case가 더 작은 값이 되었으며 같은 case 인 경우 나중에 들어온 값이 더 낮은 값으로 계산되었다.
