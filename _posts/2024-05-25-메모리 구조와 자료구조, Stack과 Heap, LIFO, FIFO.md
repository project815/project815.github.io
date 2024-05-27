---
title: 메모리 구조와 자료구조, Stack과 Heap, LIFO, FIFO
description: 메모리 구조에 나오는 Stack과 Heap에 대한 내용을 정리한 내용입니다. Stack과 Heap이라는 용어가 메모리 구조와 자료구조에서 개념을 혼용하여 사용하는 경우가 종종 있는 것 같습니다. 메모리구조의 Stack은 LIFO, Heap은 FIFO라는 글들을 봤습니다. 하지만 메모리 구조 상 Heap 존재하는 데이터가 FIFO라는 말은 틀린 말입니다.
author: songminseok
date: 2024-05-27 14:41:00 +09:00
categories:
  - 용어정리
tags:
  - 메모리구조
  - Stack
  - Heap
  - LIFO
  - FIFO
pin: true
math: true
mermaid: true
---

## 메모리공간
메모리 공간(RAM)은 크게 **코드(Code), 데이터(Data), 스택(Stack), 힙(Heap) 영역**으로 나뉜다.
![](https://media.vlpt.us/images/seungho1216/post/4fe85243-36d7-49ca-a8fa-d825ed6d04d7/%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0.png)

### ▶︎코드 영역 (Code Segment)
**코드 영역**은 프로그램의 실행 코드(명령어)가 저장되는 영역
+ 기계어로 번역된 프로그램 코드, 즉 실행 명령어들이 저장
+ CPU가 실행할 명령어들을 순서대로 가져와서 실행

### ▶︎ 데이터(Data) 영역
**전역 변수와 정적 변수(static)**가 할당되는 영역
- 프로그램 시작 시에 할당되고, 프로그램이 종료될 때까지 유지

### ▶︎ 힙(Heap) 영역
동적 메모리 할당을 위해 사용되는 영역
+ 동적 할당: `malloc`, `calloc`, `realloc` 등의 함수로 동적 할당되며, `free` 함수로 해제
	+ 즉, 사용자(프로그래머)에 의해 관리될 필요가 있다.
- 응용 프로그램이 종료될 때까지 메모리가 유지되기 때문에 사용하고 난 후 반드시 매모리 해제를 해줘야 한다.(memory leak 발생), **Java에서는 가비지 컬렉터가 자동으로 해제**한다
- 프로그램 실행 중에 크기가 변할 수 있는 데이터를 저장합니다. 예를 들어, 동적 배열, 연결 리스트, 트리 구조 등이 힙에 저장
- 영역 중 유일하게 **런타임시 크기가 결정**
- **참조형(Reference Type) 데이터 타입을 갖는 객체(인스턴스), 배열** 등이 저장되는 공간,  
    단 힙 영역에 있는 오브젝트들을 가리키는 레퍼런스 변수는 스택에 적재
- <font color="#ff0000">메모리의 낮은 주소부터 할당되는 선입선출(FIFO) 구조</font>
-> 프로그래머가 메모리 동적 할당하는 영역이 왜 선입선출이라고 표현을 한걸까?? 결론부터 말하면 메모리구조 힙영역은 선입선출 구조가 아님.

### ▶︎ 스택(Stack) 영역
프로그램이 자동으로 사용하는 임시 메모리 영역
- 함수 호출 시 생성되는 **지역 변수와 매개 변수**가 저장되는 영역
- 함수 호출과 함께 자동으로 할당되고, 함수가 종료되면 자동으로 해제
- 메모리의 높은 주소부터 할당되는 **후입선출(LIFO) 구조**


---
## 자료구조
###### Stack : LIFO
###### Queue : FIFO
###### Heap : 완전이진트리(비선형구조)

## 메모리 공간의 Heap영역은 선입선출 구조다?
> 메모리 공간의 Heap영역은 선입선출 구조가 아니다!!!
> <br>
{: .prompt-danger }
> 몇몇 블로그에서 메모리공간 Heap영역은 선입선출이라는 표현을 사용을 했다. 나도 그렇게 생각했다.
> <br>
> 나는 자료구조의 스택과 메모리공간의 스택이 후입선출구조라는 방식이 같다는 점 때문에
> 자료구조의 힙과 메모리공간의 힙은 반대로 선입선출이라고 유추해 생각했다.
> <br>
> 하지만 이것은 거짓! 아래 그와 관련된 글을 찾아보고, 번역한 글이다.
> <br>
> Chat gpt에게 질문을 했었는데, 연속되고 집요한 질문에도 heap영역은 FIFO인가?라는 질문에는 아니라고 답했다.
{: .prompt-info }

### 스택과 힙에 대해서
The Stack
: 스택

The Stack is a region of memory in RAM that is used to store data that is needed temporarily by a program. This includes function arguments, local variables, return addresses, and other temporary values. The Stack is managed automatically by the computer's processor, which pushes and pops data onto and off the stack as needed.
: 스택은 프로그램의 임시 데이터를 저장하는 메모리영역입니다.
: 함수 매개변수, 지역변수, 반환 주소 및 임시 값이 이곳에 해당한다.
: 스택은 필요에 따라 데이터를 넣고 뺄 수 있으며, 컴퓨터 프로세서에 의해 자동으로 관리된다.

The Stack is a Last In, First Out (LIFO) data structure, meaning that the last item pushed onto the stack is the first item popped off the stack. This makes the Stack ideal for managing function calls and nested subroutines, as each new function call pushes its local variables and return address onto the top of the stack, and each function return pops them off again.
: 스택은 LIFO(후입선출)데이터 구조이다. 즉, 스택의 마지막 데이터는 스택에서 꺼내는 가장 첫번째 데이터라는 것을 의미한다.
: 이것은 함수 호출과 중첩된 서브루틴(재귀함수를 의미하느 듯)을 관리하는 데 이상적이다. 함수 호출 시 지역변수와 반환주소를 스택의 최상단에 푸쉬하고, 함수가 반환될 때 스택에서 함수의 지역변수와 반환함수를 다시 꺼낸다.

The Heap
: 힙

The Heap is another region of memory in RAM that is used to store data that needs to persist beyond the lifetime of a single function call. This includes dynamically allocated memory, such as objects, arrays, and other data structures, which are not bound to a specific scope or lifetime. Unlike the Stack, the Heap is not managed automatically by the processor, but rather by the programmer, who is responsible for allocating and deallocating memory as needed.
: 힙은 단일 함수의 생명주기 이후에도 유지될 필요가 있는 데이터를 저장하는 메모리영역이다.
: 생명주기 또는 특정 범위에 정해져있지 않은 데이터 구조, 배열, 객체와 같이 동적 메모리가 이곳에 해당한다.
: 스택과 달리, 힙은 프로세서에 의해 자동으로 관리되지 않고, 필요에 따라 메모리 할당 및 해체를 프로그래머가 담당한다.

The Heap is a more flexible data structure than the Stack, as it allows for dynamic resizing and allocation of memory at runtime. However, managing the Heap requires more careful attention and can be more error-prone, as the programmer must ensure that all allocated memory is properly released when it is no longer needed.
: 힙은 런타임에 메모리의 사이즈를 유동적으로 바꿀 수 있고, 할당할 수 있으므로, 스택보다 데이터 구조가 유연한 데이터이다.
: 그러나 힙 관리는 더 세심한 주의가 요구된다. 프로그래머 반드시 모든 할당한 메모리를 더이상 필요하지 않을 때 해제되어지도록 보장해줘야 함으로 오류가 발생하기 쉽다.

---
### Heap이 FIFO인가?
FIFO (first in = first out) is a queue, a list where you add things at the tail and remove them from the head. (LIFO (last in = first out) is a stack, where you both add and remove from the top.)
: 선입선출은 꼬리(tail)에 항목을 추가하고 머리(head)에 제거하는 열이다.
: LIFO(Last in Frist out)은 스택, top에서 추가 삭제가 이루어진다.

A (max) heap is, compared to these, a very strange beast. You put things in a vaguely descending order, with the nth element always greater than or equal to the ones at 2n and 2n+1 (if they exist). Then you remove things (successive maximum values) from the apex (element 1) and add more things to be sorted at the base/end. After every operation, you promote internal elements if it is necessary to maintain the relative order. By keeping it relatively, rather than completely, ordered, you can use it to sort things with minimal wasted time.
: 완전 힙은 매우 이상한~
: 이것은 막연한(?) 내림차순이다. n번째 요소는 항상 2n과 2n+1의 요소보다 크거나 같도록 하는 순서임.
: 그리고 정점(요소 1)에서 연속적인 가장 큰 값을 제거하고, base/end에서 정렬될 것을 더 추가한다. 
: 모든 작업 후, 상대적 순서를 유지할 필요가 있는 경우 승격시킨다.
: 이 과정은 완전히까지는 아니고, 상대적으로 순서를 유지시킨다. 그러므로써 적은 비용으로 정렬을 사용할 수 있다.

One of the uses for such a thing, other than a complete sort, is a simple priority ‘queue’. New items enter, with various levels of importance. You always pick the most important one first, but new data is free to arrive without making you sort all over from scratch.
: 완전한 정렬 이외에 이러한 용도인 것 중 하나는 우선순위 큐이다. 여러 중요도에 따라 새로운 아이템(데이터)가 들어온다. 
: 정렬하지 않고도 새로운 데이터가 비용없이 할당될수도 있지만 항상 중요도가 있는 것이 먼저 뽑힌다.

---
### Heap란?
In addition, heap memory is not associated with a specific function or process. **The data in heap memory is not arranged in any specific pattern and can be reached in any order**. Throughout a program’s runtime, only useful areas of memory are retained in heap memory.
: 게다가 힙 메모리는 특정 함수 또는 프로세스를 할당하지 않는다. 힙메모리는 특정 패턴으로 정렬되지 않고 어떤 순서에서든 접근할 수 있다. 게다가 런타임에, 오직 메모리의 유용한 영역만 힙 메모리에 유지되어진다.


## 정리
사실 이 글의 시작은 나의 작은 오해에서 비롯됐다.
메모리구조의 스택과 힙, 자료구조의 스택과 힙을 동일시 한 것에서 비롯됐다.
하지만 논리적으로 힙영역은 프로그래머가 자동할당해체하는 영역이며, 메모리 상에 어디에 위치하고 있는지 알 수 없다.
그러나 설명해서 FIFO 구조이다? 위치를 모르는데 가능한 이야기가 아니다.

이 의문을 파헤치다 보니 메모리구조와 자료구조의 특징을 보다 명확하게 구분 지어 생각할 수 있게 됐다.

## 참조 및 기타 참조할 만한 글(메모리 구조에 대한 설명)
<https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/>
<br>
<http://bucarotechelp.com/computers/architecture/81051201.asp#google_vignette>
<br>
<https://www.spiceworks.com/tech/devops/articles/fifo-vs-lifo/>
<br>
<https://www.baeldung.com/cs/memory-stack-vs-heap>
<br>
<https://www.quora.com/Is-FIFO-a-heap>