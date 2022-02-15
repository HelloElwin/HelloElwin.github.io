---
layout: post
title: First Post, Test Post
categories: General
date: 2022-02-14
---

## Some mathmatical technique of proof

This is a test post. However, it's not only for test, because:

> Even if you are writing a test post, you can learn a lot. *Lu Xun*

### 1 Proof by nonsense

Note that $$ 1+1 = 2 $$, therefore we have

$$
\sum_{i=1}^{100}i = \sum_{i=1}^1 1 + \sum_{i=1}^2 1 + \cdots + \sum_{i=1}^{99}1 + \sum_{i=1}^{100}1 = 5050
$$

### 2 Proof by code

We run the following code:

```cpp
#include <iostream>

int main() {

	int ans = 0;

	for (int i = 0; i <= 100; i++) {
		ans += i;
	}

	cout<<ans;

	return 0;
}
```
The output is $$5050$$, which implies that the sum is definitely $$5050$$.

### 3 Proof by contradiction

Let us assume that the sum is not 5050, then we oberve that this contradicts with the former proofs, therefore the sum is exactly 5050!
