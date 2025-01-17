---
title : "[스택/큐]제로(C)"
expert : "백준 10773 스택문제"
toc: true
toc_sticky: true
categories:
  - Blog
tags:
  - Blog
---

## 1.문제 설명

> 나코더 기장 재민이는 동아리 회식을 준비하기 위해서 장부를 관리하는 중이다.
> 
> 재현이는 재민이를 도와서 돈을 관리하는 중인데, 애석하게도 항상 정신없는 재현이는 돈을 실수로 잘못 부르는 사고를 치기 일쑤였다.
> 
> 재현이는 잘못된 수를 부를 때마다 0을 외쳐서, 가장 최근에 재민이가 쓴 수를 지우게 시킨다.
> 
> 재민이는 이렇게 모든 수를 받아 적은 후 그 수의 합을 알고 싶어 한다. 재민이를 도와주자!



## 2.입력

> 첫 번째 줄에 정수 K가 주어진다. (1 ≤ K ≤ 100,000)
> 
> 이후 K개의 줄에 정수가 1개씩 주어진다. 정수는 0에서 1,000,000 사이의 값을 가지며, 정수가 "0" 일 경우에는 가장 최근에 쓴 수를 지우고, 아닐 경우 해당 수를 쓴다.
> 
> 정수가 "0"일 경우에 지울 수 있는 수가 있음을 보장할 수 있다.



## 3.출력

> 재민이가 최종적으로 적어 낸 수의 합을 출력한다. 최종적으로 적어낸 수의 합은 231-1보다 작거나 같은 정수이다.



### 예제입력1

```
4
3
0
4
0
```

### 예제출력1

```
0
```

### 예제입력2

```
10
1
3
5
4
0
0
7
0
0
6
```

### 예제출력2

```
7
```


## 4.알고리즘 설명

이 문제에서 짚고가야 하는 포인트를 정리해봤다

- 첫번째 입력받는 숫자만큼 숫자를 입력받는다

- 0보다 큰 숫자가 입력되면 그 숫자를 스택에 넣는다

- 0이 입력되면 스택에서 숫자 하나를 뺀다

- 첫번째 입력받은 숫자만큼 수를 입력받고나면 스택에 남아있는 숫자를 모두 더해 결과값으로 출력한다

- 첫번째 수 k의 범위가 100000까지 가능하므로 스택의 크기는 1000000으로 만든다

이를 이용해 코드를 작성해보면 먼저 count라는 int형 변수를 만들어 첫번째 숫자를 입력받고 count만큼 for문을 돌려 숫자를 입력받는다. 입력받은 숫자를 int형 변수 value에 저장하고 0보다 클 경우 value값을 push, 0일경우엔 pop을 수행한다. 이후에 스택의 값을 for문으로 모두 더하고 그 값을 출력한다



## 5.코드

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>
#include <string.h>
#define MAX_STACK_SIZE 100000

int stack[MAX_STACK_SIZE];
int top =-1;

int isFull(){
    if(top >= MAX_STACK_SIZE -1){
        return 1;
    }
    return 0;
}

int isEmpty(){
    if(top==-1){
        return 1;
    }
    return 0;
}
void push(int data){
    if(!isFull()){
        top++;
        stack[top] = data;
    }
}
int pop(){
    if(!isEmpty()){
        return stack[top--];
    }
    return 0;
}
int main(){
    int count=0, sum=0;
    int value=0;
    scanf("%d",&count);
    for(int i=0;i<count;i++){
        scanf("%d", &value);
        if(value>0)
            push(value);
        else
            pop();
    }
    for(int i=0;i<=top;i++){
        sum+=stack[i];
    }
    printf("%d",sum);    
    return 0;
}
```
## 6.마치며

조건문을 이용해 스택에 값을 저장하고 더하는 과정에서 c언어로 입출력을 구현하는 것이 조금 까다로웠지만 알고리즘 자체는 그렇게 어렵지 않았다.
