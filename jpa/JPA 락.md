# JPA 락

- 기본적으로 JPA의 영속성 컨텍스트를 적절히 활용하면 데이터베이스의 트랜잭션 격리 수준이 `READ COMMITTED`여도 애플리케이션 레벨에서 `REPEATABLE READ`가 가능합니다.

## 갱신 손실 문제

- 데이터베이스 트랜잭션의 범위를 넘어서는 문제이므로 트랜잭션만으로는 해결할 수 없습니다.
- 해결 방법
  - 마지막 커밋만 인정하기
  - 최초 커밋만 인정하기
  - 충돌하는 갱신 내용 병합하기

## 낙관적 락 (Optimistic Lock)

- 대부분의 트랜잭션이 충돌하지 않는다고 가정하는 방식입니다.
- DB 락이 아닌 JPA가 제공하는 버전 관리 기능을 사용합니다.
- 트랜잭션 커밋 시점에 충돌을 확인합니다.
- 발생 가능 예외
  - JPA 예외 : `OptimisticLockException`
  - 스프링 예외 추상화 : `ObjectOptimisticLockingFailureException`

### @Version

- 엔터티에 버전 관리용 필드를 추가하고 해당 어노테이션을 붙여 사용합니다.
- 주요 특징
  - 엔터티를 수정 시, 버전이 자동으로 증가합니다.
  - 조회 시점과 수정 시점의 버전이 다르면 예외가 발생합니다. (최초 커밋만 인정)
  - 임베디드 타입과 값 타입 컬렉션은 논리적인 개념상 해당 엔터티의 값이므로 수정하면 엔터티의 버전이 증가합니다.
  - 연관관계 필드는 외래 키를 관리하는 연관관계의 주인 필드를 수정할 때만 버전이 증가합니다.
  - 벌크 연산은 버전 처리를 무시합니다. (수동 증가 필요)

## 비관적 락 (Pessimistic Lock)

- 트랜잭션 충돌이 발생한다고 가정하고 DB 락 기능을 사용합니다.
- 데이터 수정 시점에 즉시 트랜잭션 충돌을 감지할 수 있습니다.
- 발생 가능 예외
  - JPA 예외 : `PessimisticLockException`
  - 스프링 예외 추상화 : `PessimisticLockingFailureException`

## JPA 락 옵션 (LockModeType)

### OPTIMISTIC

- `@Version`만 적용했을 때는 엔터티를 수정해야 버전을 체크하지만, 이 옵션을 추가하면 엔터티의 수정 없이 단순히 조회만 해도 버전 체크를 수행합니다.
- `Dirty Read`, `Non-Repeatable Read` 방지

### OPTIMISTIC_FORCE_INCREMENT

- 엔터티를 수정하지 않아도 커밋 시점에 강제로 버전을 증가시킵니다.
- 엔터티를 수정하면 총 2번의 버전 증가가 나타날 수 있습니다.
- 연관관계의 주인이 아닌 엔터티의 필드 수정 시에는 버전이 증가하지 않는데, 이 옵션을 사용함으로써 논리적 단위의 엔터티 묶음을 버전 관리할 수 있습니다.

### PESSIMISTIC_WRITE

- 일반적으로 비관적 락은 이 옵션을 뜻합니다.
- 배타락을 사용합니다. (`SELECT … FOR UPDATE`)

### PESSIMISTIC_READ

- 공유락을 사용합니다. (`SELECT … FOR SHARE`)

### PESSIMISTIC_FORCE_INCREMENT

- 비관적 락중 유일하게 버전 정보를 사용합니다.
- 버전 정보를 강제로 증가시킵니다.

## 참고

- [자바 ORM 표준 JPA 프로그래밍](https://www.yes24.com/product/goods/19040233)