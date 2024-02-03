백준 14425.문자열

for문 돌리기

```
N,M=map(int,input().split())
S=[input() for _ in range(N)]
word=[input() for _ in range(M)]
cnt=0
for i in word:
    if i in S:
        cnt+=1
print(cnt)
```

set으로 filter사용

```

a, b = map(int, input().split())
_set = set([input() for _ in range(a)])
print(len(list(filter(lambda v : v in _set, [input() for _ in range(b)]))))
```
