## 이분탐색
```python
s = [10,12,13,14,18,20,25,27,30,35,40,45,47]
s
```
```
[10, 12, 13, 14, 18, 20, 25, 27, 30, 35, 40, 45, 47]
```
```python
def binary_search(s,low,high, k):
    if low > high:
        return -1
    else:
        mid = (low + high) // 2
        if s[mid] == k:
            return mid
        else:
            if s[mid] < k:
                return binary_search(s,mid+1,high, k)
            else:
                return binary_search(s,low, mid-1, k)
```

```python
binary_search(s,0, len(s)-1,30)
```
```
8
```

## 합병정렬

재귀적으로 구현한 합병정렬

```python
s = [27, 10, 12, 20, 25, 13, 15, 22]
s
```
```
[27, 10, 12, 20, 25, 13, 15, 22]
```

```python
def merge(l, r):
    s = []
    i = j = 0
    while(i < len(l) and j < len(r)):
        if(l[i] < r[j]):
            s.append(l[i])
            i += 1
        else:
            s.append(r[j])
            j += 1
    if(i < len(l)):
        s += l[i:]
    else:
        s += r[j:]
    return s    
```

```python
def merge_sort(s):
    n = len(s)
    if (n <= 1) :
        return s
    else:
        mid = n // 2
        l = merge_sort(s[:mid])
        r = merge_sort(s[mid:])
        return merge(l,r)
merge_sort(s)
```
```
[10, 12, 13, 15, 20, 22, 25, 27]
```


