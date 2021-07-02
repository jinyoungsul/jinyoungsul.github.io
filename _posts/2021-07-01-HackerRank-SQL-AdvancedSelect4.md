---
title : HackerRank-AdvancedSelect-Binary Tree Nodes

tags:
    - sql
categories:
    - sql 
date: '2021-07-01'

---

# Binary Tree Nodes

You are given a table, _BST_, containing two columns: _N_ and _P,_ where _N_ represents the value of a node in _Binary Tree_, and _P_ is the parent of _N_.

![](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)


Write a query to find the node type of  _Binary Tree_  ordered by the value of the node. Output one of the following for each node:

-   _Root_: If node is root node.
-   _Leaf_: If node is leaf node.
-   _Inner_: If node is neither root nor leaf node.

**Sample Input**

![](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)

**Sample Output**

```
1 Leaf
2 Inner
3 Leaf
5 Root
6 Leaf
8 Inner
9 Leaf
```

**Explanation**

The  _Binary Tree_  below illustrates the sample:

**My solution**
```sql
SELECT DISTINCT(bst1.N), CASE WHEN bst1.P IS NULL THEN 'Root'
            WHEN bst2.N IS NULL THEN 'Leaf'
            ELSE 'Inner'
            END
FROM BST bst1 LEFT OUTER JOIN BST bst2
ON bst1.N=bst2.P
ORDER BY bst1.N ASC;
```

**Most vote solution**
```sql
SELECT N, CASE WHEN P IS NULL THEN 'Root'
               WHEN N IN (SELECT DISTINCT(P) FROM BST) THEN 'Inner'
               ELSE 'Leaf'
          END
FROM BST
ORDER BY N;
```


![](https://i.imgur.com/CU1BnKl.png)


