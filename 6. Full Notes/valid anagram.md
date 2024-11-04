Given two strings `s` and `t`, return `true` if the two strings are anagrams of each other, otherwise return `false`.

An **anagram** is a string that contains the exact same characters as another string, but the order of the characters can be different.

**Example 1:**

```java
Input: s = "racecar", t = "carrace"

Output: true
```

Copy

**Example 2:**

```java
Input: s = "jar", t = "jam"

Output: false
```

Copy

**Constraints:**

- `s` and `t` consist of lowercase English letters.

```
class Solution {

    /**

     * @param {string} s

     * @param {string} t

     * @return {boolean}

     */

    isAnagram(s, t) {

        if(s.length !== t.length){

            return false

        }

  

       const map_s = {}

        const map_t = {}

  

        for(let i = 0; i < s.length; i++){

            map_s[s[i]] = (map_s[s[i]] || 0) + 1;

            map_t[t[i]] = (map_t[t[i]] || 0) + 1;

        }

  

        for(const key in map_s){

            if(map_s[key] !== map_t[key]){

                return false;

            }

        }

        return true;

}

}
```