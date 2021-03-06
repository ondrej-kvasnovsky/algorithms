# Trie

[Trie](https://en.wikipedia.org/wiki/Trie) \(pronounce try\) a.k.a. digital tree, a.k.a. radix tree, a.k.a prefix tree is a tree structure that can be used to implement fast lookup of strings.

![](/assets/250px-Trie_example.svg.png)

Lets implement trie using a hash map.

```
import java.util.*;

class Trie {

    TrieNode root = new TrieNode();

    public void add(String word) {
        // 1. take each char from word and try to find it in root
        // 2. if found, move the current to another element it found
        // 3. if not found, create new value
        TrieNode current = root;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            Map<Character, TrieNode> children = current.children;
            if (children.containsKey(c)) {
                current = children.get(c);
            } else {
                TrieNode newNode = new TrieNode();
                newNode.value = c;
                children.put(c, newNode);
                current = newNode;
            }
        }
    }

    public boolean contains(String word) {
        // go char by char from word
        // look for each char in values in root
        // if found, set current to the found one
        // if not found, return false
        // at the end, return true
        TrieNode current = root;
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if (current.children.containsKey(c)) {
                current = current.children.get(c);
            } else {
                return false;
            }
        }
        return true;
    }

    public List<String> findByPrefix(String prefix) {
        // go char by char from prefix
        // when at the last position, get all variations from that place using

        TrieNode current = root;
        StringBuilder path = new StringBuilder();
        for (int i = 0; i < prefix.length(); i++) {
            char c = prefix.charAt(i);
            if (current.children.containsKey(c)) {
                path.append(c);
                current = current.children.get(c);
            }
        }

        List<String> results = new ArrayList<>();
        // if current has children, create all combinations (depth first)
        current.children.forEach((key, value) -> {
            StringBuilder b = new StringBuilder(path);
            generateCombinations(b, value, results);
        });

        return results;
    }

    private void generateCombinations(StringBuilder prefix, TrieNode current, List<String> results) {
        if (current == null) return;
        StringBuilder newWord = new StringBuilder();
        newWord.append(prefix);
        newWord.append(current.value);
        results.add(newWord.toString());
        current.children.forEach((key, value) -> {
            StringBuilder b = new StringBuilder(newWord);
            generateCombinations(b, value, results);
        });
    }

    public String asString() {
        return toString(root);
    }

    public String toString(TrieNode node) {
        if (node == null) return null;
        StringBuilder result = new StringBuilder();
        result.append(node.value);
        result.append(" ");
        node.children.forEach((c, n) -> {
            result.append(toString(n));
        });
        return result.toString();
    }
}

class TrieNode {
    char value;
    Map<Character, TrieNode> children = new HashMap<>();
}
```

We can try to use the Trie class. Insert couple of words and then check if a word is in. Also we try to get all words by a prefix.

```
public class TrieDemo {
    public static void main(String... args) {
        Trie trie = new Trie();

        trie.add("hi");
        trie.add("hello");
        trie.add("word");
        trie.add("world");

        System.out.println(trie.asString());

        System.out.println(trie.contains("h")); // true
        System.out.println(trie.contains("hi")); // true
        System.out.println(trie.contains("hi5")); // false
        System.out.println(trie.contains("world")); // true

        List<String> foundWords1 = trie.findByPrefix("h");
        System.out.println(Arrays.toString(foundWords1.toArray()));

        List<String> foundWords2 = trie.findByPrefix("wo");
        System.out.println(Arrays.toString(foundWords2.toArray()));
    }
}
```

Here is the output.

```
  w o r d l d h e l l o i 
true
true
false
true
[he, hel, hell, hello, hi]
[wor, word, worl, world]
```

Other implementation using an array

```
class TrieNode {
    // change this value to adapt to different cases
    public static final N = 26;
    public TrieNode[] children = new TrieNode[N];
}
```



