# Error와 Exception 

## 계층 구조

<img src = "https://github.com/user-attachments/assets/97abc082-2d50-4dfa-87ad-7baa05fcfdae" width="400" height="800">

## Error

- `Error`는 메모리 부족(OutOfMemoryError)이나 스택오버플로우(StackOverflowError)와 같이, 일단 발생하면 복구할 수 없는 심각한 문제입니다.
(일반적으로 처리하지 않습니다.)

## Exception

- `Exception`은 프로그램 내에서 발생할 수 있는 문제로, 예외 처리를 통해 해결할 수 있습니다. 

### Checked Exception

- `Checked Exception`은 `RuntimeException` 클래스를 상속받지 않은 `Exception` 클래스들입니다.
- 복구 가능성이 있는 예외이므로 컴파일 단계에서 명시적인 예외 처리(`catch 문`, `throws`)를 해야 합니다.
<br> (처리하지 않으면 `컴파일러`가 에러가 발생시킵니다.)

### Unchecked Exception

- `Unchecked Exception`은 `RuntimeException` 클래스를 상속받는 `Exception` 클래스들입니다. 
- 복구 가능성이 없는 예외이므로 명시적인 예외 처리를 하지 않습니다.
<br> (`컴파일러`가 예외 처리를 강제하지 않습니다.)
- 이 때문에 개발자가 예외를 실수로 누락할 수 있다는 문제점이 있습니다.

### @Transactional

- 선언적 트랜잭션 안에서 발생하는 `Error`와 `Unchecked Exception`은 롤백이 되지만, `Checked Exception`은 롤백이 되지 않습니다.

## throw vs throws

- `throw`는 예외를 실제로 던질 때 사용합니다.
- `throws`는 메서드 선언부에 사용하여 해당 메서드가 던질 수 있는 예외를 선언할 때 사용합니다. 

## 참고

[이미지 참고](https://www.programcreek.com/2009/02/diagram-for-hierarchy-of-exception-classes/)