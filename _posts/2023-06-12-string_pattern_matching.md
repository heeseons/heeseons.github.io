---
title: '문자열 검색 알고리듬: 브루트-포스, 보이어-무어, KMP'
categories: [Computer Science, Data Structures]
tags: [data structures, brute-force, boyer-moore, kmp]
math: 'True'
---

## Pattern Matching

### 브루트-포스 알고리듬 (Brute-Force Algorithm)
문자열의 가능한 모든 위치에서 패턴을 비교하여 일치하는 부분 탐색\
시간 복잡도: $O(nm)$ ($n$: 텍스트의 길이, $m$: 패턴의 길이)

```
Procedure BruteForceMatch(T,P)
	Input text T of size n and pattern P of size m
	Output i such that T[i, i+m]=P, or -1 if no such i exists
	for i ← 0, ..., n-m  //패턴 P를 비교할 텍스트 T 내부 위치
		j ← 0  //패턴 P의 인덱스
	while j<m and T[i+j]=P[j]  //한 글자씩 비교
		j ← j+1
	if j=m  //패턴 발견
		return i
	else
		break while loop  //mismatch
	return -1  //no match
```
{: file="psuedo code"}

<br>

### 보이어-무어 알고리듬 (Boyer-Moore Algorithm)
* **거울 휴리스틱** (Looking-glass heuristic): 패턴의 뒤에서부터 앞으로 비교
* **문자 점프 휴리스틱** (Character-jump heuristic): 일치하지 않는 문자의 다음 비교 위치를 미리 계산하여 점프

시간 복잡도: $O(m+s)$ ($m$: 패턴의 길이, $s$:∑의 크기, ∑: 문자열 알파벳)
> 예: $T=ababcdaac$ → $∑=\( \{a,b,c,d\} \)$
{: .prompt-tip}

```
Procedure BoyerMooreMatch(T, P, ∑)
	last←last occurrence function w.r.t. P, ∑  //T 내부 이동거리 결정
	i ← m-1  //T 내부 포인터(인덱스)
	j ← m-1  //P 내부 포인터(인덱스)
	repeat
		if T[i]=P[j]
			if j=0  //패턴 발견
				return i
			else
				i ← i-1  //Looking-glass heuristic
				j ← j-1
		else
		l ← last(T[i])  //T[i]가 마지막으로 등장하는 인덱스 l
		i ← i + m - min(j,1+l)  //Character-jump heuristic
		j ← m-1
	until i>n-1
	return -1
```
{: file="psuedo code"}

<br>

### KMP 알고리듬 (Knuth-Morris-Pratt's Algorithm)
패턴 $P$를 전처리하여 얻은 **접두사(prefix)/접미사(suffix)** 활용\
시간 복잡도: $O(n+m)$ ($n$: 텍스트의 길이, $m$: 패턴의 길이)

```
Procedure KMPMatch(T, P)
	F ← failure function of P  //접두사, 접미사 저장
	i, j ← 0
	while i<n
		if T[i]=P[j]
			if j=m-1
				return i-j
			else
				i ← i+1
				j ← j+1
		else
			if j>0
				j ← F(j-1)
			else
			 i ← i+1
	return -1
```
{: file="psuedo code"}

<br>

---

## 참고
* Data Structures and Algorithms in JAVA Fourth Edition *(Michael T. Goodrich, Roberto Tamassia)*
