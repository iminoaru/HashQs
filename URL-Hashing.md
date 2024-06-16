
# Hashmap-based URL Shortener
## Description:

You are tasked with implementing a URL shortener service similar to Bitly. Your goal is to design a system that shortens long URLs into unique short codes and retrieves the original URL when given its short code.

Write two functions:

1.  `String shortenURL(String longURL)` - This function generates a unique short code for the given `longURL` and returns it. The short code should be unique and can be alphanumeric.
    
2.  `String retrieveURL(String shortCode)` - This function takes a short code `shortCode` and returns the original `longURL` associated with it.
    
You can assume that the long URLs are unique and the short codes should be unique for each generated URL.

## Testcases:
### Test Case 1:

Input: longURL = "https://app.100xdevs.com" 

Output: "shortURL/abc123"

### Test Case 2:

Input: longURL = "https://gaud.vercel.app" 

Output: "shortURL/xyz456"

### Test Case 3:

Input: longURL = "https://www.facebook.com" 

Output: "shortURL/def789"

### Test Case 4:

Input: longURL = "https://www.apple.com" 

Output: "shortURL/ghi456"

### Test Case 5:

Input: longURL = "https://www.microsoft.com" 

Output: "shortURL/jkl012"


#### NOTE:
URL will differ on every run as its random.

## Constraints:

-   The short codes should be unique and can contain alphanumeric characters.
-   The generated short codes will have a maximum length of 10 characters.
-   The `shortenURL` function should handle URLs with up to 1000 characters.

## JAVA solution

```java
import java.util.*;

public class URLShortener {
    private static Map<String, String> urlToShortCodeMap = new HashMap<>();
    private static Map<String, String> shortCodeToUrlMap = new HashMap<>();
    private static int counter = 0;

    public static String shortenURL(String longURL) {
        String shortCode = "shortURL/" + generateShortCode();
        urlToShortCodeMap.put(longURL, shortCode);
        shortCodeToUrlMap.put(shortCode, longURL);
        return shortCode;
    }

    public static String retrieveURL(String shortCode) {
        return shortCodeToUrlMap.getOrDefault(shortCode, "URL not found.");
    }

    private static String generateShortCode() {
        return Integer.toString(counter++);
    }

    public static void main(String[] args) {
        String longURL = "https://www.google.com";
        String shortCode = shortenURL(longURL);
        System.out.println(shortCode);
        System.out.println(retrieveURL(shortCode));
    }
}
```

## PYTHON solution

```python
import random
import string

class URLShortener:
    def __init__(self):
        self.url_to_short_code_map = {}
        self.short_code_to_url_map = {}
        self.counter = 0
        self.alphabet = string.ascii_letters + string.digits

    def shorten_url(self, long_url):
        short_code = "shortURL/" + self.generate_short_code()
        self.url_to_short_code_map[long_url] = short_code
        self.short_code_to_url_map[short_code] = long_url
        return short_code

    def retrieve_url(self, short_code):
        return self.short_code_to_url_map.get(short_code, "URL not found.")

    def generate_short_code(self):
        code = ''.join(random.choices(self.alphabet, k=6))
        return code


shortener = URLShortener()
long_url = "https://app.100xdevs.com"
short_code = shortener.shorten_url(long_url)
print(short_code)
print(shortener.retrieve_url(short_code))
```

## C++ solution

```cpp
#include <iostream>
#include <unordered_map>
#include <random>
#include <string>

using namespace std;

class URLShortener {
private:
    unordered_map<string, string> urlToShortCodeMap;
    unordered_map<string, string> shortCodeToUrlMap;
    int counter;
    string alphabet;

public:
    URLShortener() : counter(0), alphabet("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789") {}

    string shortenURL(string longURL) {
        string shortCode = "shortURL/" + generateShortCode();
        urlToShortCodeMap[longURL] = shortCode;
        shortCodeToUrlMap[shortCode] = longURL;
        return shortCode;
    }

    string retrieveURL(string shortCode) {
        return shortCodeToUrlMap.find(shortCode) != shortCodeToUrlMap.end() ? shortCodeToUrlMap[shortCode] : "URL not found.";
    }

private:
    string generateShortCode() {
        string code;
        for (int i = 0; i < 6; ++i) {
            code += alphabet[rand() % alphabet.size()];
        }
        return code;
    }
};

int main() {
    URLShortener shortener;
    string longURL = "https://www.google.com";
    string shortCode = shortener.shortenURL(longURL);
    cout << shortCode << endl;
    cout << shortener.retrieveURL(shortCode) << endl;
    return 0;
}
```

