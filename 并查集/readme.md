# 并查集模板
```
"""
***并查集（union find）：
1.需要实现的模块
class Element：包装元素
find_head：找到当前element的代表element
union：将两个元素所在的集合合并
is_same_set：判断两个元素是否在同一个集合中
2.需要利用的数据结构：
element dic：存每个元素对应的element
father dic：存每个element的父亲element
rank dic：存每个结合代表element的子element个数
"""


class Element:
    def __init__(self, val):
        self.val = val


class UnionFind:
    def __init__(self, v):
        self.v = v
        self.element_dic = {}
        self.head_dic = {}
        self.rank_dic = {}
        for cur_v in v:
            cur_element = Element(cur_v)
            self.element_dic[cur_v] = cur_element
            self.head_dic[cur_element] = cur_element
            self.rank_dic[cur_element] = 1

    def __find_head(self, element):
        stack = []
        if element in self.head_dic:
            while self.head_dic[element].val != element.val:
                stack.append(element)
                element = self.head_dic[element]
            while stack:
                cur_element = stack.pop()
                self.head_dic[cur_element] = element
        return element

    def union(self, a, b):
        if a in self.element_dic and b in self.element_dic:
            a_head = self.__find_head(self.element_dic[a])
            b_head = self.__find_head(self.element_dic[b])
            if a_head.val == b_head.val:
                return
            else:
                a_head_rank = self.rank_dic[a_head]
                b_head_rank = self.rank_dic[b_head]
                if a_head_rank <= b_head_rank:
                    self.head_dic[a_head] = b_head
                    self.rank_dic[b_head] += self.rank_dic[a_head]
                    self.rank_dic.pop(a_head)
                else:
                    self.head_dic[b_head] = a_head
                    self.rank_dic[a_head] += self.rank_dic[b_head]
                    self.rank_dic.pop(b_head)

    def is_same_det(self, a, b):
        if a in self.element_dic and b in self.element_dic:
            a_head = self.__find_head(self.element_dic[a])
            b_head = self.__find_head(self.element_dic[b])
            if a_head.val == b_head.val:
                return True
            else:
                return False


if __name__ == '__main__':
    a = [1, 2, 3, 4, 5]
    groups = [[1, 2], [1, 3], [4, 5]]
    test = [[1, 2], [2, 3], [1, 4]]

    u = UnionFind(a)
    for i in range(len(groups)):
        u.union(groups[i][0], groups[i][1])
        print(u.is_same_det(test[i][0], test[i][1]))
    head_dic = u.head_dic
    rank_dic = u.rank_dic
    print("look head dic:")
    for k, v in head_dic.items():
        print(k.val, v.val)
    print("look rank dic:")
    for k, v in rank_dic.items():
        print(k.val, v)
 """
 output:
 True
True
False
look head dic:
1 2
2 2
3 2
4 5
5 5
look rank dic:
2 3
5 2
"""
```
