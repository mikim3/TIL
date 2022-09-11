# 글을 쓰게된 이유

[https://www.notion.so/80000coding/Python-27440f94daba431684cf47266f7d7fea]

[https://github.com/rlaalstn0107/Study/commit/74a87286df1a39e400d48c76cf7115fbe34c53c6](https://github.com/rlaalstn0107/Study/commit/74a87286df1a39e400d48c76cf7115fbe34c53c6)

[https://github.com/rlaalstn0107/Study/commit/106101b73dbc9017c030c61bbbe092db4ac67ea3](https://github.com/rlaalstn0107/Study/commit/106101b73dbc9017c030c61bbbe092db4ac67ea3)

배열로 하면 어떻게 탐색해야 빠를까 고민이 필요한 문제가 딕셔너리 자료형을 사용하는것 만으로 알고리즘 고민 없이 해결이 되어서 문제를 풀때 이 생각을 자주 활용하는게 좋겠다는 생각이 들어서 글을 쓰게 되었다.

## 예시

숫자카드2 문제에 배열을 이용해서 푼 경우다. 첫번째는 시간초과가 떴고(소스 자세히 볼 필요 없음)

```jsx
import sys
input = sys.stdin.readline

n = int(input())
mycard = list(map(int,input().split()))
mycard.sort()
m = int(input())
question = list(map(int,input().split()))

def binary_search(array,target,start,end):
    if start > end:
        return None
    mid = (start + end) // 2
    if array[mid] == target:
        return array[start:end + 1].count(target)
    elif array[mid] < target:
        return binary_search(array, target, mid+1, end)
    else:
        return binary_search(array, target, start, mid-1)

for i in range(len(question)):
    a = binary_search(mycard, question[i], 0, len(mycard)-1)
    if a is not None:
        print(a, end = ' ')
    else:
        print(0, end=' ')
```

두번째는 성공은 했으나 3600ms가 떴다.

```jsx
from sys import stdin
_ = stdin.readline()
N = sorted(map(int,stdin.readline().split()))
_ = stdin.readline()
M = map(int,stdin.readline().split())

def binary(n, N, start, end):
    if start > end:
        return 0
    m = (start+end)//2
    if n == N[m]:
        return N[start:end+1].count(n)
    elif n < N[m]:
        return binary(n, N, start, m-1)
    else:
        return binary(n, N, m+1, end)

n_dic = {}
for n in N:
    start = 0
    end = len(N) - 1
    if n not in n_dic:
        n_dic[n] = binary(n, N, start, end)

print(' '.join(str(n_dic[x]) if x in n_dic else '0' for x in M ))
```

사실 이 문제를 처음 풀때는 2중 for 문으로 모든 경우의 수를 계산하면서 다 풀었다. 당연히 시간초과가 떴다.

그리고 그 후에 딕셔너리로 풀어서 800ms 정도가 떴다.(딕셔너리를 쓰는 결정을 하는 것 만으로 구현만 하니 소스가 간단해졌다.)

```jsx
n = int(input())
mycard = list(map(int,input().split()))
m = int(input())
question = list(map(int,input().split()))

dic_count = {}

for card in mycard:
    if card in dic_count:
        dic_count[card] += 1
    else:
        dic_count[card] = 1
for target in question:
    result = dic_count.get(target)
    if result == None:
        print(0, end = " ")
    else:
        print(result, end = " ")
```

배열을 쓰면 탐색알고리즘에 대해 고민이 필요하지만 딕셔너리는 그런 고민자체가 필요 없어지는 경우가 많았다.

# 결론

탐색이 느릴때는 그냥 딕셔너리를 써보자

> **Life is Short, You Need Python *Dictionary*!**
> 

왜 딕셔너리가 빠르냐면 

[https://analytics4everything.tistory.com/m/180](https://analytics4everything.tistory.com/m/180)

자세한 설명은 생략
