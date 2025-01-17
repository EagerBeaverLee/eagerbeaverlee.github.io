---
title : "[스택/큐]올바른 괄호(C)"
expert : "Programmers 올바른 괄호"
toc: true
toc_sticky: true
categories:
  - Blog
tags:
  - Blog
---

## 1.문제 설명

> 괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어
> 
> - "()()" 또는 "(())()" 는 올바른 괄호입니다.
> - ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.
> 
> '(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.


## 2.제한사항

> - 문자열 s의 길이 : 100,000 이하의 자연수
> - 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.



## 3.입출력 예

| S        | answer |
| -------- | ------ |
| "()()"   | true   |
| "(())()" | true   |
| ")()("   | false  |
| "(()("   | false  |



## 4.알고리즘 설명

이 문제의 핵심은 소괄호가 어지럽게 섞여있어도 결국에 닫혀있으면 된다. 즉 여는괄호 "(" 와 닫는괄호 ")" 의 짝이 맞으면 조건을 만족한다는 뜻이다. 따라서 입력받은 문자열에서 다음과 같은 조건을 만족하면 이 문제를 해결할 수 있다. 



- 지금 스택 제일 위 문자가 ")"일 경우
  
  다음에 올 문자가 "(" 이거나 ")" 일 경우 모두 닫혀있는 상태를 만들 수 없으므로 다음에 올 문자를 무조건 스택에 추가한다

- 지금 스택 제일 위 문자가 "("이고, 다음 올 문자가 ")" 일 경우
  
  괄호가 닫힌상태를 만족하기 때문에 제일 위 "(" 문자를 pop을 이용하여 제거한다

- 지금 스택 제일 위 문자가 "("이고, 다음 올 문자가 "(" 일 경우
  
  닫힌상태를 만족하지 않기 때문에 다음 올 문자"("를 스택에 넣는다.



이 3가지를 조건문으로 만들어 문자열 s를 처음부터 마지막까지 스캔한 후 스택에 문자열이 남아있으면 전체가 닫힌상태가 아니므로 "false"를, 문자열이 남아있지 않으면 닫힌상태를 만족함으로 "true"를 반환하도록 코드를 작성하였다.



## 5.코드

```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>
#include <string.h>
#define MAX_STACK_SIZE 100000

char stack[MAX_STACK_SIZE];
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

void push(char data){
    if(!isFull()){
        top++;
        stack[top] = data;
    }
}
char pop(){
    if(!isEmpty()){
        return stack[top--];
    }
}

// 파라미터로 주어지는 문자열은 const로 주어집니다. 변경하려면 문자열을 복사해서 사용하세요.
bool solution(const char* s) {
    bool answer = false;
    push(s[0]);
    for(int i=1;i<strlen(s);i++){
        if(stack[top]==')'){
            push(s[i]);
            continue;
        }
        else if(s[i]==')')
            pop();
        else
            push(s[i]);
    }
    if(top==-1)
        answer = true;
    return answer;
}
```



## 6.마치며

이 문제에서는 효율성테스트도 함께 진행을 하였고, 내가 작성한 코드는 2가지 케이스 모두 시간초과로 실패판정을 받았다. 스택에 대한 이해를 좀 더 높여서 효율성테스트까지 통과할 수 있는 코드를 추후에 작성해볼 예정이다.  
