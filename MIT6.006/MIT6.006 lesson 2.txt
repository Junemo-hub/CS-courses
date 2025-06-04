MITOCW 알고리즘 강의 2강 요약
주제: 데이터 구조와 동적 배열

1. 강의 개요

오늘의 주제는 알고리즘이 아니라 "데이터 구조"임
핵심 목표는 시퀀스(Sequence) 인터페이스를 다양한 데이터 구조로 구현하는 것

2. 인터페이스 vs 데이터 구조

인터페이스: 무엇을 할 수 있는가 (API, 기능 정의)
데이터 구조: 어떻게 그것을 구현할 것인가 (실제 구조, 방법)

3. Sequence 인터페이스 (정적 시퀀스)

기능: build, length, iter, get_at(i), set_at(i)
구현: 정적 배열 (static array)
연속된 메모리 공간 사용, 메모리 : array of w-bit words(연속된 bit들의 모임이 메모리)
array = consecutive chunk
get/set은 O(1)
전체 순회는 O(n) 
memory allocation model은 세타(n)이래
크기 변경 불가

4. 동적 시퀀스 기능 추가

insert_at(i, x), delete_at(i)
insert_first, insert_last
delete_first, delete_last

5. 연결 리스트 (Linked List)

각 노드는 item + next 포인터
insert_first, delete_first는 O(1)
get_at(i), insert_at(i)는 O(n)
랜덤 접근이 느림
tail 포인터를 저장하면 get_last는 O(1)

6. 정적 배열의 한계

insert/delete 시 shifting 필요 → O(n)
크기 확장 불가 → 새 배열 할당 필요 → O(n)

7. 동적 배열 (Dynamic Array)

배열의 크기를 여유 있게 할당 (size >= n)
일반적으로 size = 2 * n
insert_last 시 공간 여유 있으면 O(1)
공간 부족 시 배열 확장 + 복사 → O(n)

8. 암화타이즈드 분석 (Amortized Analysis)

n번의 insert_last 연산 → 총 O(n)
평균 O(1)
delete_last도 유사하게 O(1) 암화타이즈드
insert_at(i)는 여전히 O(n)

9. 시간 복잡도 비교

연산	Static Array	Linked List	Dynamic Array
get/set_at(i)	O(1)	O(n)	O(1)
insert_first	O(n)	O(1)	O(n)
insert_last	O(n)	O(n)	O(1) amortized
insert_at(i)	O(n)	O(n)	O(n)
delete_last	O(n)	O(n)	O(1) amortized

10. 결론

정적 배열은 랜덤 접근에 강함
연결 리스트는 앞쪽 삽입/삭제에 강함
동적 배열은 평균적으로 가장 효율적인 선택
Python의 list는 동적 배열로 구현되어 있음


*** 이해를 못했다고 생각한 부분
Word RAM 모델이란? w ≥ log n
amortized O(1)은 무슨 뜻이야? 진짜 O(1)하고 뭐가 달라?

Tail 포인터를 저장한다는 게 무슨 말