---
sidebar_position: 1
---

# A - Circuit Math 

🔗 Link: https://open.kattis.com/problems/circuitmath

## Short Description

Given a [postfix expression](https://web.stonehill.edu/compsci/CS104/Stuff/Infix%20and%20%20postfix%20expressions.pdf) of a boolean circuit and the current true/ false values of up to 26 variables.
Evaluate the expression and output the result.

## Analysis

Use an array to fast-lookup the variables and use a stack to simulate the evaluation.

## Sample Code

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs groupId="lang">
<TabItem value="py" label="Python 3">

```py showLineNumbers
n = int(input())
value = list(map(lambda x: True if x == "T" else False, input().split(" ")))
expression = input().split(" ")
stack = []

for op in expression:
  if op == "*":
    X = stack.pop()
    Y = stack.pop()
    stack.append(X & Y)
  elif op == "+":
    X = stack.pop()
    Y = stack.pop()
    stack.append(X | Y)
  elif op == "-":
    X = stack.pop()
    stack.append(not X)
  else:
    stack.append(value[ord(op) - ord('A')])

print("T" if stack[0] == True else "F")
```

</TabItem>
<TabItem value="cpp" label="C++">

```cpp showLineNumbers
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;
  vector<bool> value(n);
  for (int i = 0; i < n; i++) {
    string x;
    cin >> x;
    if (x == "T") {
      value[i] = true;
    } else {
      value[i] = false;
    }
  }

  string op;
  stack<bool> st;
  while (cin >> op) {
    if (op == "*") {
      bool X = st.top(); st.pop();
      bool Y = st.top(); st.pop();
      st.push(X & Y);
    } else if (op == "+") {
      bool X = st.top(); st.pop();
      bool Y = st.top(); st.pop();
      st.push(X | Y);
    } else if (op == "-") {
      bool X = st.top(); st.pop();
      st.push(!X);
    } else {
      st.push(value[op[0]-'A']);
    }
  }
  cout << (st.top()? "T":"F") << '\n';
}
```

</TabItem>
</Tabs>
