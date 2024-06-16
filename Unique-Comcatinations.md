
# Unique Character Concatenation
## Description:

You are given a list of strings. Your task is to concatenate all the strings such that the resulting string has the maximum number of unique characters.
Write a function `int maxUniqueConcat(List<String> strings)` that returns an integer representing the maximum number of unique characters 
in the concatenated string.

## Testcases:
### Test Case 1:

Input: strings = ["abc", "def", "ghi"]

Output: 9

### Test Case 2:

Input: strings = ["abc", "bcd", "cde"]

Output: 5

### Test Case 3:

Input: strings = ["a", "b", "c", "d"]

Output: 4

### Test Case 4:

Input: strings = ["abcd", "zfxh", "iakl"]

Output: 12

### Test Case 5:

Input: strings = ["abc", "ab", "a"]

Output: 3

## Constraints:

-   The number of strings will be between 1 and 100.
-   Each string will consist only of lowercase English letters ('a' to 'z') and have a maximum length of 100.

## JAVA solution

```java
import java.util.*;

public class Main {
    public static int maxUniqueConcat(List<String> strings) {
        Map<Character, Integer> charCount = new HashMap<>();
        for (String s : strings) {
            for (char c : s.toCharArray()) {
                charCount.put(c, charCount.getOrDefault(c, 0) + 1);
            }
        }
        return charCount.size();
    }

    public static void main(String[] args) {
        List<String> strings = Arrays.asList("abc", "def", "ghi");
        System.out.println(maxUniqueConcat(strings));
    }
}
```

## PYTHON solution

```python
def maxUniqueConcat(strings):
    char_count = {}
    for s in strings:
        for c in s:
            char_count[c] = char_count.get(c, 0) + 1
    return len(char_count)

strings = ["abc", "def", "ghi"]
print(maxUniqueConcat(strings))
```

## C++ solution

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>

using namespace std;

int maxUniqueConcat(vector<string>& strings) {
    unordered_map<char, int> charCount;
    for (const string& s : strings) {
        for (char c : s) {
            charCount[c]++;
        }
    }
    return charCount.size();
}

int main() {
    vector<string> strings = {"abc", "def", "ghi"};
    cout << maxUniqueConcat(strings) << endl; 
    return 0;
}
```

