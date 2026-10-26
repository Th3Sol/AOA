
# AOA Practical Programs

## Quick Navigation

1. [Insertion Sort](#1a-insertion-sort)
2. [Selection Sort](#1b-selection-sort)
3. [Insertion and Selection Sort](#1c-insertion-sort-and-selection-sort-in-one-program)
4. [Binary Search](#2-binary-search)
5. [Minimum and Maximum using Divide and Conquer](#3-minimum-and-maximum-using-divide-and-conquer)
6. [Quick Sort](#4-quick-sort)
7. [Prim's Algorithm (MST)](#5-prims-algorithm-minimum-spanning-tree-mst)
8. [0/1 Knapsack using Dynamic Programming](#6-01-knapsack-using-dynamic-programming)
9. [Floyd-Warshall Algorithm](#7-floyd-warshall-algorithm)
10. [N-Queen using Backtracking](#8-n-queen-problem-using-backtracking)
11. [Job Sequencing with Deadlines](#9-job-sequencing-with-deadlines-greedy)
12. [Rabin-Karp String Matching](#10-rabin-karp-string-matching)

---

## 1(a). Insertion Sort

<a id="1a-insertion-sort"></a>

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[50], n, i, j, key;
    clrscr();

    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    for(i = 1; i < n; i++)
    {
        key = a[i];
        j = i - 1;

        while(j >= 0 && a[j] > key)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }

    printf("Sorted array: ");
    for(i = 0; i < n; i++)
        printf("%d ", a[i]);

    getch();
}
```

## 1(b). Selection Sort

<a id="1b-selection-sort"></a>

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[50], n, i, j, min, temp;
    clrscr();

    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    for(i = 0; i < n - 1; i++)
    {
        min = i;

        for(j = i + 1; j < n; j++)
            if(a[j] < a[min])
                min = j;

        temp = a[i];
        a[i] = a[min];
        a[min] = temp;
    }

    printf("Sorted array: ");
    for(i = 0; i < n; i++)
        printf("%d ", a[i]);

    getch();
}
```
### 1(c). Insertion Sort and Selection Sort in One Program

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[50], n, i, j, key, min, temp, choice;
    clrscr();

    printf("1. Insertion Sort\n");
    printf("2. Selection Sort\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);

    if(choice != 1 && choice != 2)
    {
        printf("Invalid choice");
        getch();
        return;
    }

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");
    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    if(choice == 1)
    {
        for(i = 1; i < n; i++)
        {
            key = a[i];
            j = i - 1;

            while(j >= 0 && a[j] > key)
            {
                a[j + 1] = a[j];
                j--;
            }

            a[j + 1] = key;
        }
    }
    else
    {
        for(i = 0; i < n - 1; i++)
        {
            min = i;

            for(j = i + 1; j < n; j++)
                if(a[j] < a[min])
                    min = j;

            temp = a[i];
            a[i] = a[min];
            a[min] = temp;
        }
    }

    printf("Sorted array: ");
    for(i = 0; i < n; i++)
        printf("%d ", a[i]);

    getch();
}
```

## 2. Binary Search

<a id="2-binary-search"></a>

**Note:** Enter elements in ascending order.

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[50], n, i, key, low, high, mid;
    clrscr();

    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    printf("Enter element to search: ");
    scanf("%d", &key);

    low = 0;
    high = n - 1;

    while(low <= high)
    {
        mid = (low + high) / 2;

        if(a[mid] == key)
            break;
        else if(a[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }

    if(low <= high)
        printf("Element found at position %d", mid + 1);
    else
        printf("Element not found");

    getch();
}
```

## 3. Minimum and Maximum using Divide and Conquer

<a id="3-minimum-and-maximum-using-divide-and-conquer"></a>

```c
#include <stdio.h>
#include <conio.h>

int a[50], min, max;

void find(int l, int r)
{
    int mid;

    if(l == r)
    {
        if(a[l] < min) min = a[l];
        if(a[l] > max) max = a[l];
        return;
    }

    mid = (l + r) / 2;
    find(l, mid);
    find(mid + 1, r);
}

void main()
{
    int n, i;
    clrscr();

    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    min = max = a[0];
    find(0, n - 1);

    printf("Minimum = %d\nMaximum = %d", min, max);
    getch();
}
```

## 4. Quick Sort

<a id="4-quick-sort"></a>

```c
#include <stdio.h>
#include <conio.h>

int a[50];

void quick(int low, int high)
{
    int i, j, pivot, temp;

    if(low >= high)
        return;

    pivot = a[low];
    i = low + 1;
    j = high;

    while(i <= j)
    {
        while(i <= high && a[i] <= pivot)
            i++;

        while(j > low && a[j] > pivot)
            j--;

        if(i < j)
        {
            temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    }

    a[low] = a[j];
    a[j] = pivot;

    quick(low, j - 1);
    quick(j + 1, high);
}

void main()
{
    int n, i;
    clrscr();

    printf("Enter number of elements: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
        scanf("%d", &a[i]);

    quick(0, n - 1);

    printf("Sorted array: ");
    for(i = 0; i < n; i++)
        printf("%d ", a[i]);

    getch();
}
```

## 5. Prim's Algorithm — Minimum Spanning Tree (MST)

<a id="5-prims-algorithm-minimum-spanning-tree-mst"></a>

Enter the weighted adjacency matrix. Use `0` where no edge exists.

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[10][10], visited[10] = {0};
    int n, i, j, edges = 0, min;
    int u = 0, v = 0, cost = 0;

    clrscr();

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter adjacency matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++)
            scanf("%d", &a[i][j]);

    visited[0] = 1;
    printf("MST edges:\n");

    while(edges < n - 1)
    {
        min = 999;

        for(i = 0; i < n; i++)
            if(visited[i])
                for(j = 0; j < n; j++)
                    if(!visited[j] && a[i][j] > 0 &&
                       a[i][j] < min)
                    {
                        min = a[i][j];
                        u = i;
                        v = j;
                    }

        if(min == 999)
        {
            printf("Graph is disconnected");
            getch();
            return;
        }

        printf("%d - %d : %d\n", u + 1, v + 1, min);
        cost += min;
        visited[v] = 1;
        edges++;
    }

    printf("Total cost = %d", cost);
    getch();
}
```

## 6. 0/1 Knapsack using Dynamic Programming

<a id="6-01-knapsack-using-dynamic-programming"></a>

This program supports capacity up to 100.

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int w[20], p[20], dp[21][101];
    int n, cap, i, j;

    clrscr();

    printf("Enter number of items: ");
    scanf("%d", &n);

    printf("Enter weights:\n");
    for(i = 1; i <= n; i++)
        scanf("%d", &w[i]);

    printf("Enter profits:\n");
    for(i = 1; i <= n; i++)
        scanf("%d", &p[i]);

    printf("Enter capacity (max 100): ");
    scanf("%d", &cap);

    for(i = 0; i <= n; i++)
        for(j = 0; j <= cap; j++)
        {
            if(i == 0 || j == 0)
                dp[i][j] = 0;
            else if(w[i] <= j)
            {
                if(p[i] + dp[i-1][j-w[i]] >
                   dp[i-1][j])
                    dp[i][j] = p[i] + dp[i-1][j-w[i]];
                else
                    dp[i][j] = dp[i-1][j];
            }
            else
                dp[i][j] = dp[i-1][j];
        }

    printf("Maximum profit = %d", dp[n][cap]);
    getch();
}
```

## 7. Floyd-Warshall Algorithm

<a id="7-floyd-warshall-algorithm"></a>

Use `999` to represent no direct edge between vertices.

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int a[10][10], n, i, j, k;

    clrscr();

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter adjacency matrix (999 for no edge):\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < n; j++)
            scanf("%d", &a[i][j]);

    for(k = 0; k < n; k++)
        for(i = 0; i < n; i++)
            for(j = 0; j < n; j++)
                if(a[i][k] != 999 && a[k][j] != 999 &&
                   a[i][k] + a[k][j] < a[i][j])
                    a[i][j] = a[i][k] + a[k][j];

    printf("Shortest distance matrix:\n");
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < n; j++)
            printf("%d ", a[i][j]);
        printf("\n");
    }

    getch();
}
```

## 8. N-Queen Problem using Backtracking

<a id="8-n-queen-problem-using-backtracking"></a>

This version solves the 4-Queen problem.

```c
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>

int x[10], n = 4;

int place(int row, int col)
{
    int i;

    for(i = 1; i < row; i++)
        if(x[i] == col ||
           abs(x[i] - col) == abs(i - row))
            return 0;

    return 1;
}

int solve(int row)
{
    int col, i;

    if(row > n)
    {
        for(i = 1; i <= n; i++)
        {
            for(col = 1; col <= n; col++)
                printf("%c ", x[i] == col ? 'Q' : '-');
            printf("\n");
        }
        return 1;
    }

    for(col = 1; col <= n; col++)
        if(place(row, col))
        {
            x[row] = col;
            if(solve(row + 1))
                return 1;
        }

    return 0;
}

void main()
{
    clrscr();

    if(!solve(1))
        printf("No solution");

    getch();
}
```

## 9. Job Sequencing with Deadlines — Greedy

<a id="9-job-sequencing-with-deadlines-greedy"></a>

Each job takes one unit of time.

```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int id[20], d[20], p[20], slot[20];
    int n, i, j, k, temp, maxd = 0, profit = 0;

    clrscr();

    printf("Enter number of jobs: ");
    scanf("%d", &n);

    for(i = 0; i < n; i++)
    {
        id[i] = i + 1;
        printf("Enter deadline and profit: ");
        scanf("%d%d", &d[i], &p[i]);

        if(d[i] > maxd)
            maxd = d[i];
    }

    for(i = 0; i < n - 1; i++)
        for(j = i + 1; j < n; j++)
            if(p[i] < p[j])
            {
                temp = p[i]; p[i] = p[j]; p[j] = temp;
                temp = d[i]; d[i] = d[j]; d[j] = temp;
                temp = id[i]; id[i] = id[j]; id[j] = temp;
            }

    if(maxd > n)
        maxd = n;

    for(i = 0; i < maxd; i++)
        slot[i] = 0;

    for(i = 0; i < n; i++)
        for(k = d[i] - 1; k >= 0 && k < maxd; k--)
            if(slot[k] == 0)
            {
                slot[k] = id[i];
                profit += p[i];
                break;
            }

    printf("Selected jobs: ");
    for(i = 0; i < maxd; i++)
        if(slot[i] != 0)
            printf("J%d ", slot[i]);

    printf("\nMaximum profit = %d", profit);
    getch();
}
```

## 10. Rabin-Karp String Matching

<a id="10-rabin-karp-string-matching"></a>

```c
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
    char text[100], pat[50];
    int n, m, i, j, found = 0;
    int h = 1, p = 0, t = 0, d = 256, q = 101;

    clrscr();

    printf("Enter text: ");
    gets(text);

    printf("Enter pattern: ");
    gets(pat);

    n = strlen(text);
    m = strlen(pat);

    if(m == 0 || m > n)
    {
        printf("Pattern not found");
        getch();
        return;
    }

    for(i = 0; i < m - 1; i++)
        h = (h * d) % q;

    for(i = 0; i < m; i++)
    {
        p = (d * p + pat[i]) % q;
        t = (d * t + text[i]) % q;
    }

    for(i = 0; i <= n - m; i++)
    {
        if(p == t)
        {
            for(j = 0; j < m; j++)
                if(text[i+j] != pat[j])
                    break;

            if(j == m)
            {
                printf("Pattern found at position %d\n", i + 1);
                found = 1;
            }
        }

        if(i < n - m)
        {
            t = (d * (t - text[i] * h) +
                 text[i + m]) % q;

            if(t < 0)
                t += q;
        }
    }

    if(!found)
        printf("Pattern not found");

    getch();
}
```

---
