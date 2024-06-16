# Efficient Document Classification
## Description:
You are given a list of documents, where each document is represented as a string of words. 
Your task is to group the indexes of all the similar documents given and return them as an array. 
Specifically, you need to group the documents that have the same word frequency distribution.

Write a function `List<List<Integer>> classifyDocuments(String[] documents)` that returns a list of lists. 
Each sublist should contain the indices of the documents that have the same word frequency distribution.
Return the List of Lists in any order.

## Testcases:
Test Case 1:

Input: documents = ["data structures and algorithms", "algorithms and data structures", "machine learning", "learning machine"]

Output: [[0, 1], [2, 3]]

Test Case 2:

Input: documents = ["the quick brown fox", "quick the brown fox", "lazy dog", "dog lazy", "jumped over the lazy dog"]

Output: [[0, 1], [2, 3], [4]]

Test Case 3:

Input: documents = ["one two three", "four five six", "seven eight nine", "one two three"]

Output: [[0, 3], [1], [2]]

Test Case 4:

Input: documents = ["hello world", "world hello", "hello", "world"]

Output: [[0, 1], [2], [3]]

Test Case 5:

Input: documents = ["a b c", "c b a", "a a b b", "a b"]

Output: [[0, 1], [2], [3]]

## Constraints:
The number of documents will be between 1 and 10.
Each document will contain between 1 and 5 words.
Words in a document are separated by single spaces.
Words consist of lowercase English letters and have a maximum length of 30 characters.


## JAVA solution
```java
import java.util.*;

public class Main {
    public static List<List<Integer>> classifyDocuments(String[] documents) {
        Map<String, List<Integer>> freqMap = new HashMap<>();
        for (int i = 0; i < documents.length; i++) {
            String[] words = documents[i].split(" ");
            Map<String, Integer> wordCount = new HashMap<>();
            for (String word : words) {
                wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
            }
            String key = wordCount.toString();
            if (!freqMap.containsKey(key)) {
                freqMap.put(key, new ArrayList<>());
            }
            freqMap.get(key).add(i);
        }
        return new ArrayList<>(freqMap.values());
    }

    public static void main(String[] args) {
        String[] documents = {"data structures and algorithms", "algorithms and data structures", "machine learning", "learning machine"};
        System.out.println(classifyDocuments(documents));  
    }
}

```

## PYTHON solution

```python
from collections import defaultdict

def classifyDocuments(documents):
    freq_map = defaultdict(list)
    for index, doc in enumerate(documents):
        words = doc.split()
        word_count = {}
        for word in words:
            word_count[word] = word_count.get(word, 0) + 1
        key = tuple(sorted(word_count.items()))
        freq_map[key].append(index)
    return list(freq_map.values())


documents = ["data structures d algorithms", "algorithms and data structures", "machine learning", "learning machine"]
print(classifyDocuments(documents))  

```

## C++ solution

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <map>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<vector<int>> classifyDocuments(vector<string>& documents) {
    unordered_map<string, vector<int>> freqMap;
    for (int i = 0; i < documents.size(); i++) {
        istringstream iss(documents[i]);
        string word;
        map<string, int> wordCount;
        while (iss >> word) {
            wordCount[word]++;
        }
        stringstream ss;
        for (const auto& pair : wordCount) {
            ss << pair.first << ":" << pair.second << ",";
        }
        string key = ss.str();
        freqMap[key].push_back(i);
    }
    vector<vector<int>> result;
    for (const auto& pair : freqMap) {
        result.push_back(pair.second);
    }
    return result;
}

int main() {
    vector<string> documents = {"data structures  algorithms", "algorithms and data structures", "machine learning", "learning machine"};
    vector<vector<int>> result = classifyDocuments(documents);
    for (const auto& group : result) {
        for (int index : group) {
            cout << index << " ";
        }
        cout << endl;
    }
    
}

```


