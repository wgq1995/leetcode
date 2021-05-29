# 二分查找模板
```
# 二分查找
def binary_search(a, k):
    if not a:
        return False
    if k < a[0] or k > a[-1]:
        return False
    n = len(a)
    l, r = 0, n-1
    while l <= r:
        mid = (l + r) // 2
        if a[mid] == k:
            return True
        elif a[mid] < k:
            l = mid+1
        else:
            r = mid
    return False


if __name__ == '__main__':
    a = [4, 5]
    k = 5
    if binary_search(a, k):
        print("找到了k")
    else:
        print("没找到k")
```
