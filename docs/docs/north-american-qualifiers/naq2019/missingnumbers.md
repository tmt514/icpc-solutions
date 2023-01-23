---
sidebar_position: 4
---

# D - Missing Numbers

🔗 Link: https://open.kattis.com/problems/missingnumbers

## Short Description

See the link above.

## Analysis

We can keep the input in a list (or a set).
Then, for each number we check if it is inside the list.

## Sample Code

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs groupId="lang">
<TabItem value="py" label="Python 3">

```py showLineNumbers
n = int(input())
S = set([int(input()) for i in range(n)])
if max(S) == n:
  print("good job")
else:
  for i in range(1, max(S)+1):
    if i not in S:
      print(i)
```

</TabItem>
<TabItem value="cpp" label="C++">

```cpp showLineNumbers
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;
  vector<int> a(n);
  for (int i = 0; i < n; i++) cin >> a[i];
  set<int> s(a.begin(), a.end());
  if (a.back() == n) {
    cout << "good job\n";
  } else {
    for (int i = 1; i <= a.back(); i++)
      if (s.find(i) == s.end()) {
        cout << i << '\n';
      }
  }
  return 0;
}
```

</TabItem>
<TabItem value="ocaml" label="OCaml">

```ocaml showLineNumbers
let numbers = Hashtbl.create 200;;

let line = read_line () in 
let n = int_of_string (line) in
for i = 1 to n do (
  let v = int_of_string (read_line ()) in
  Hashtbl.add numbers "input" v;
) done;

let rec max_elem lst = match lst with
  |[] -> 0
  |x::xs -> max x (max_elem xs)
in

let lst = Hashtbl.find_all numbers "input" in
let m = max_elem lst in
if n == m then
  Printf.printf "good job\n"
else
  for i = 1 to m do (
    let pred x = (if x = i then true else false) in
    if List.exists pred lst then () else
      Printf.printf "%d\n" i;
  ) done;
```

</TabItem>
</Tabs>
