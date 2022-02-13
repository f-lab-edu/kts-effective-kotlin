## 아이템 9 `use`를 사용하여 리소스를 닫아라
- close 메서드를 통해 명시적으로 닫아야 하는 리소스가 있다.
    - InputStream, OutputStream
    - java.sql.Connection
    - java.io.Reader
    - java.new.Socket, java.util.Scanner
- 명시적으로 close  메서드를 호출해 주는 것이 좋다.
- 전통적으로는 리소스를 다음과 같이 try-finally 블록을 사용해서 처리했음        
    ```kotlin
    try {
        return reader.lineSequence().sumBy {it.lentgh}
    } finally {
        reader.close()
    }
    ```
        
    - 리소스를 닫을 때 예외가 발생할 수 있는데, 이러한 예외를 따로 처리하지 않기 때문에 좋은 코드가 아님
    - 또한 try나 finllay 블록 내부에서 오류가 발생하면 둘 중 하나만 전파됨
    - 아래와 같이 리팩터링 할 수 있음
        
    ```kotlin
    BufferReader(FileReader(path)).use { reader ->
        return reader.lineSequence().sumBy { it.length }
    } 
    ```        
- use 내부
    - try와 finally 각각에서 오류를 핸들링 해줌
    - 직접 구현하려면 매우 복잡하고 코드가 길어짐
        
    ```kotlin
    @InlineOnly
    @RequireKotlin("1.2", versionKind = RequireKotlinVersionKind.COMPILER_VERSION, message = "Requires newer compiler version to be inlined correctly.")
    public inline fun <T : Closeable?, R> T.use(block: (T) -> R): R {
        contract {
            callsInPlace(block, InvocationKind.EXACTLY_ONCE)
        }
        var exception: Throwable? = null
        try {
            return block(this)
        } catch (e: Throwable) {
            exception = e
            throw e
        } finally {
            when {
                apiVersionIsAtLeast(1, 1, 0) -> this.closeFinally(exception)
                this == null -> {}
                exception == null -> close()
                else ->
                    try {
                        close()
                    } catch (closeException: Throwable) {
                        // cause.addSuppressed(closeException) // ignored here
                    }
            }
        }
    }
    ```
        
- useLines 함수
    - 메모리에 파일의 내용을 한줄씩만 유지하므로 대용량 파일도 효율적으로 처리 가능
    - 다만 파일의 줄을 한번만 사용할 수 있다는 단점 존재함
        
    ```kotlin
    fun countCharInFile(path:String): Int {
        File(path).useLines { lines ->
        	return lines.sumBy { it.length }
        } 
    }
    ```
        
- 정리
    - use를 사용하면 Closeable/AutoCloseable을 구현한 객체를 쉽고 안전하게 처리 가능함
    - 또한 파일을 처리할 대는 파일을 한줄씩 읽어들이는 useLines를 사용하는 것이 좋음