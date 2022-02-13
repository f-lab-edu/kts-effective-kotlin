## 아이템 7 결과 부족이 발생할 경우 null과 Failure를 사용하라
- 결과가 부족한 상황?
  - 서버로부터 데이터를 읽어 들이려고 했는데 네트워크 오류로 받지 못한 경우
  - 조건에 맞는 요소가 없는 경우
  - 텍스트를 파싱해서 객체를 만들려고 했는데 텍스트의 형식이 맞지 않는 경우
  - 이러한 상황 처리하는 메커니즘은 두가지
  - null또는 실패를 나타내는 sealed 클래스
  - 예외를 throw
  - 조슈아 블로크 (이펙티브 자바)
    - 일단 예외는 **정보를 전달하는 방법으로 사용해서는 안됨**
    - 예외는 **잘못된 특별한 상황을 나타내야 하고 처리되어야** 한다.
- 왜냐?
  - 많은 개발자가 예외를 전파되는 과정을 추적 못함
  - 코틀린의 모든 예외는 unchecked 예외임
  - 예외는 예외적인 상황을 처리하기 위해서 만들어졌으므로 명시적인 테스트만큼 빠르게 동작하지 않음
  - try-catch 블록 내부에 코드를 배치하면 컴파일러 최적화가 제한됨
- null을 처리해야한다면 safe call이나 Elvis 연산자 사용 가능
  - safe call (?.)
        
    ```kotlin
    var str1 : String? = null
        
    var len = str1?.length
        
    println(len) // null;
    ```
        
    - elvis 엘비스 연산자
        
    ```kotlin
    var str1 : String? = null
        
    var len = str1?.length ?: -1
        
    println(len) // 결과 : -1
    ```
        
- Result와 같은 공용체(union type)를 리턴하기로 했다면 when 표현식을 사용해서 이를 처리할 수 있음
    - Result 타입 정의
        
    ```kotlin
        A discriminated union that encapsulates a successful outcome with a value of type T or a failure with an arbitrary Throwable exception.
    ```
        
    ```kotlin
        성공적인 결과를 캡슐화하거나 임의의 throwable 예외가 있는 실패를 캡슐화하는 식별된 공용체(discriminated union)입니다.
    ```
        
    - 더 알아보기 - 공용체란?
        
        ```kotlin
        Wiki : 컴퓨터 과학에서 공용체는 메모리의 동일한 위치 내에서 여러 표현이나 형식을 가질 수 있는 값입니다.
        ```
            
    - Result 타입 더 알아보기
    
    ```kotlin
    성공적인 결과를 캡슐화하거나 임의의 throwable 예외가 있는 실패를 캡슐화하는 식별된 공용체입니다.
    ```
    
    - [공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-result/)
    - 이러한 오류 처리 방식은 try-catch 블록보다 효율적이고 사용하기 쉽고 더 명확함
    - 일반적으로 두 가지 형태의 함수를 사용함
    - 하나는 예상할 수 있을때와 다른 하나는 예상할 수 없을 때 사용함
        - get : 특정 위치에 있는 요소를 추출할 때 사용함
        - getOrNull : out of range 오류가 발생할 수 있는 경우에 사용하고 발생한 경우에 null를 리턴함
    - 이외에도 getOrDefault를 사용할 수 있음
    - null이 발생할 가능성이 있다면 getOrNull등을 사용해서 무엇이 리턴되는지 예측할수 있게 하는 것이 좋음
