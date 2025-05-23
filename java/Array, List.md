# Array, List

## 배열(Array)

- 메모리에 연속적으로 데이터를 저장하는 자료구조입니다.
- 고정된 크기를 가집니다.
- 인덱스로 직접 접근이 가능합니다.
- **성능**<br><img src="https://github.com/user-attachments/assets/c986602a-2d8b-487c-b319-cec467fea223">

## 배열 리스트(ArrayList)

- 크기를 동적으로 조절하여 배열의 크기 제한 문제를 해결한 자료구조입니다.
- 내부적으로 일반 배열을 사용하고, 저장 공간이 부족하면 더 큰 크기의 배열을 할당하여 데이터를 복사합니다.

### 자바의 ArrayList
- 공간의 처음 크기는 `10`입니다.
- 저장 공간이 부족하면, 현재 크기의 `1.5`배 크기를 가진 새로운 배열을 생성하고 기존 데이터를 복사합니다.
- 이때, `System.arraycopy()`를 사용해 메모리 고속 복사 연산을 수행합니다.
- 새 배열을 참조하도록 변경하고, 기존 배열은 더 이상 참조되지 않아 `GC`의 대상이 됩니다.
- 성능은 배열과 동일합니다.

## 연결 리스트(LinkedList)

- 노드가 데이터와 다음 노드에 대한 참조를 가지는 자료구조입니다.
- 메모리를 동적으로 사용하며, 노드 간 참조를 위한 추가 메모리가 필요합니다.
- 자료구조에서 설명하는 `LinkedList`는 `단일 연결 리스트`입니다.
- **성능**<br><img src="https://github.com/user-attachments/assets/1c1cecd6-2398-4b31-b1c7-e9085842a46d">

### 자바의 LinkedList
- `이중 연결 리스트`로 구현되어 있어 양방향 탐색이 가능합니다.
- 첫 노드와 마지막 노드에 대한 참조를 모두 가집니다.
- 성능<br><img src="https://github.com/user-attachments/assets/ce267105-a878-4da8-9908-8fabe09e2715">

<br>

> 대부분은 배열 리스트의 성능이 우세하지만, 시작 위치에서의 데이터 추가나 삭제가 잦다면, 연결 리스트 사용을 고려할 수 있습니다.