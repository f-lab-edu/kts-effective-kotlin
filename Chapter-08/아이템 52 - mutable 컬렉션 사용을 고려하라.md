immutable 컬렉션 보다 mutable 컬렉션이 좋은 점은 성능적인 측면에서 더 빠르다는 부분이다.
immutable 컬렉션에 요소 추가시 새로운 컬렉션을 만들고, 여기에 요소를 추가하기 때문에 새로운 객체 생성 비용이 발생한다.

## 정리하면
내부에서는 mutable 컬렉션을 사용하고, 외부에 제공할 경우에는 immutable을 처리하는것이 좋다.

```kotlin
class Sample {
   private val _list = mutableListOf<Int>()
   val list: List<Int> = _list
}
```
