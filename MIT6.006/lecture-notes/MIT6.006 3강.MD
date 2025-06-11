# 📘 MIT 6.006 Lecture 3 요약: Sorting

## 📚 Set 인터페이스와 배열 기반 구현

### Set 인터페이스 연산
| 연산 | 설명 |
|------|------|
| `build(X)` | iterable X로부터 set 생성 |
| `len()` | 저장된 항목 개수 반환 |
| `find(k)` | 키가 k인 항목 반환 |
| `insert(x)` | 항목 추가 (기존 키면 대체) |
| `delete(k)` | 키가 k인 항목 삭제 |
| `find_min()` / `find_max()` | 최소/최대 키 항목 반환 |
| `find_next(k)` / `find_prev(k)` | k보다 큰/작은 키 중 가장 가까운 항목 반환 |

### 배열 기반 구현 비교

| 자료구조 | `find` | `insert` | `delete` | `find_min/max` |
|----------|--------|-----------|------------|-----------------|
| Unsorted Array | O(n) | O(n) | O(n) | O(n) |
| **Sorted Array** | **O(log n)** | O(n) | O(n) | **O(1)** |

---

build를 하는 데에는 n*log(n) 등으로 시간이 좀 더 걸렸던 것 같음.

## 🔀 정렬 알고리즘

### 1. 🌀 Permutation Sort
- **아이디어**: 모든 순열을 탐색해 정렬 여부 확인
- **시간 복잡도**: Ω(n! · n)
- **비고**: 비효율적 브루트 포스

```python
from itertools import permutations

def permutation_sort(A):
    for B in permutations(A):
        if is_sorted(B):
            return B


2. 🧩 Selection Sort
아이디어: 최대값을 뒤로 보내며 정렬
시간 복잡도: Θ(n²)
공간 복잡도: O(1) (제자리 정렬)

def selection_sort(A, i=None):
    if i is None: i = len(A) - 1
    if i > 0:
        j = prefix_max(A, i)
        A[i], A[j] = A[j], A[i]
        selection_sort(A, i - 1)

def prefix_max(A, i):
    if i > 0:
        j = prefix_max(A, i - 1)
        return j if A[j] > A[i] else i
    return i

3. 🔁 Insertion Sort
아이디어: 앞부분을 정렬된 상태로 유지하면서 삽입
시간 복잡도: Θ(n²)
공간 복잡도: O(1) (제자리 정렬)

def insertion_sort(A, i=None):
    if i is None: i = len(A) - 1
    if i > 0:
        insertion_sort(A, i - 1)
        insert_last(A, i)

def insert_last(A, i):
    if i > 0 and A[i] < A[i - 1]:
        A[i], A[i - 1] = A[i - 1], A[i]
        insert_last(A, i - 1)


4. 🌊 Merge Sort
아이디어: 배열을 반으로 나누어 정렬한 뒤 병합 (Two-finger merge)
시간 복잡도: Θ(n log n)
공간 복잡도: Θ(n) (비제자리 정렬)

def merge_sort(A, a=0, b=None):
    if b is None: b = len(A)
    if 1 < b - a:
        c = (a + b + 1) // 2
        merge_sort(A, a, c)
        merge_sort(A, c, b)
        L, R = A[a:c], A[c:b]
        merge(L, R, A, len(L), len(R), a, b)

def merge(L, R, A, i, j, a, b):
    if a < b:
        if j <= 0 or (i > 0 and L[i - 1] > R[j - 1]):
            A[b - 1] = L[i - 1]
            merge(L, R, A, i - 1, j, a, b - 1)
        else:
            A[b - 1] = R[j - 1]
            merge(L, R, A, i, j - 1, a, b - 1)

📐 재귀 분석 기법
Substitution Method: 해를 추측하고 대입해 증명
Recurrence Tree: 호출 구조를 트리로 그려 합산
Master Theorem: T(n) = aT(n/b) + f(n) 형태를 해결하는 공식


| 알고리즘             | 시간 복잡도     | 공간 복잡도 | 제자리 정렬 | 안정성 |
| ---------------- | ---------- | ------ | ------ | --- |
| Permutation Sort | O(n! · n)  | O(n)   | ❌      | ✅   |
| Selection Sort   | O(n²)      | O(1)   | ✅      | ❌   |
| Insertion Sort   | O(n²)      | O(1)   | ✅      | ✅   |
| Merge Sort       | O(n log n) | O(n)   | ❌      | ✅   |

