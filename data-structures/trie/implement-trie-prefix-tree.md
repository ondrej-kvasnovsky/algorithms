# Implement Trie \(Prefix Tree\)

Implement a trie with`insert`,`search`, and`startsWith`methods.

**Example:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

* You may assume that all inputs are consist of lowercase letters`a-z`
* All inputs are guaranteed to be non-empty strings.

## Solution

```
class Trie {

    static class TrieNode {
        char value;
        boolean isWord;
        Map<Character, TrieNode> children = new HashMap<>();
        TrieNode(char value) {
            this.value = value;
        }
        public String toString() {
            StringBuilder sb = new StringBuilder();
            Queue<TrieNode> queue = new LinkedList<>();
            queue.offer(this);
            while (!queue.isEmpty()) {
                int size = queue.size();
                for (int i = 0; i < size; i++) {
                    TrieNode node = queue.poll();
                    sb.append(node.value);
                    for (Map.Entry<Character, TrieNode> child : node.children.entrySet()) {
                        queue.offer(child.getValue());
                    }
                }
            }
            return sb.toString();
        }
    }

    private TrieNode root;
    
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode(' ');    
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode current = root;
        TrieNode last = null;
        int index = 0;
        while (index < word.length()) {
            char c = word.charAt(index);
            if (current.children.containsKey(c)) {
                current = current.children.get(c);
            } else {
                last = new TrieNode(c);
                current.children.put(c, last);
                current = last;
            } 
            index++;
        }
        if (current != null) {
            current.isWord = true;
        }
        //System.out.println(root);
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode current = root;
        int index = 0;
        while (index < word.length()) {
            char c = word.charAt(index);
            if (current.children.containsKey(c)) {
                current = current.children.get(c);
            } else {
                return false;
            } 
            index++;
        }
        return current.isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode current = root;
        int index = 0;
        while (index < prefix.length()) {
            char c = prefix.charAt(index);
            if (current.children.containsKey(c)) {
                current = current.children.get(c);
            } else {
                return false;
            } 
            index++;
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

Another implementation. 

```
class Trie {
    class TrieNode {
        public boolean isWord; 
        public Map<Character, TrieNode> childrenMap = new HashMap<>();
    }
    
    private TrieNode root; 

    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++){
            char c = word.charAt(i);
            if(cur.childrenMap.get(c) == null){
                // insert a new node if the path does not exist
                cur.childrenMap.put(c, new TrieNode());
            }
            cur = cur.childrenMap.get(c); 
        }
        cur.isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            if(cur.childrenMap.get(c) == null) {
                return false;
            }
            cur = cur.childrenMap.get(c);
        }
        return cur.isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode cur = root;
        for(int i = 0;i < prefix.length(); i++){
            char c = prefix.charAt(i);
            if(cur.childrenMap.get(c) == null) {
                return false;
            }
            cur = cur.childrenMap.get(c);
        }
        return true;
    }
}
```



