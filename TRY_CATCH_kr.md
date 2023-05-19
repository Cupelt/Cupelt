### TRY CATCH 예외처리

TRY CATCH는 예외처리에 뛰어난 효과를 보이는 구문입니다.

기본적인 형태는 다음과 같습니다
```
TRY
  ...Try some script
CATCH e // 'e'는 예외가 담길 변수입니다.
  ...Catch some script
FINALLY
  ...Finlly some script
ENDTRY
```

TRY CATCH문은 기본적으로 `TRY` 안에 있는 구문이 먼저 실행됩니다.</br>
`TRY` 안에 있는 스크립트에서 오류가 발생한다면 실행하던 코드를 멈추고, `CATCH` 로 넘어갑니다.

그다음 `FINALLY`는 구문의 오류와 상관없이 마지막에 실행됩니다.
+ `FINALLY`는 생략가능합니다.

TRY CATCH의 흐름을 나타내면 다음과 같습니다.
- `'Try some script' = 오류발생` -> `Catch some script` -> `Finlly some script`
- `'Try some script' = 정상실행` -> `Finlly some script`

#### 예제
이해를 돕기 위한 예제를 만들어 보겠습니다.
```
value = "a"

TRY
  #MESSAGE "TRY value > 10"
  IF value > 10
    #MESSAGE "value is greater than 10"
  ELSE
    #MESSAGE "value is less than or equal to 10"
  ENDIF
CATCH e
  #MESSAGE "Catch Some Error!!"
ENCTRY
```
위 예제는 의도적으로 오류를 만든 코드입니다.
부등호 연산자를 사용하기 위해서는 `value` 가 *"정수"* 여야 하지만 *"문자열"* 을 가지고 있어 오류가 발생하게 됩니다.

위 코드의 출력은 다음과 같습니다.
```
TRY value > 10
Catch Some Error!!
```

위 만일 `value = 1` 이라면 다음과 같이 출력됩니다.
```
TRY value > 10
value is less than or equal to 10
```
