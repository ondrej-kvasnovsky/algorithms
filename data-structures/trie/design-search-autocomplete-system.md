# Design Search Autocomplete System

Design a search autocomplete system for a search engine. Users may input a sentence \(at least one word and end with a special character`'#'`\). For**each character**they type**except '\#'**, you need to return the**top 3**historical hot sentences that have prefix the same as the part of sentence already typed. Here are the specific rules:

1. The hot degree for a sentence is defined as the number of times a user typed the exactly same sentence before.
2. The returned top 3 hot sentences should be sorted by hot degree \(The first is the hottest one\). If several sentences have the same degree of hot, you need to use ASCII-code order \(smaller one appears first\).
3. If less than 3 hot sentences exist, then just return as many as you can.
4. When the input is a special character, it means the sentence ends, and in this case, you need to return an empty list.

Your job is to implement the following functions:

The constructor function:

`AutocompleteSystem(String[] sentences, int[] times):`This is the constructor. The input is**historical data**.`Sentences`is a string array consists of previously typed sentences.`Times`is the corresponding times a sentence has been typed. Your system should record these historical data.

Now, the user wants to input a new sentence. The following function will provide the next character the user types:

`List<String> input(char c):`The input`c`is the next character typed by the user. The character will only be lower-case letters \(`'a'`to`'z'`\), blank space \(`' '`\) or a special character \(`'#'`\). Also, the previously typed sentence should be recorded in your system. The output will be the**top 3**historical hot sentences that have prefix the same as the part of sentence already typed.

**Example:**  
**Operation:**AutocompleteSystem\(\["i love you", "island","ironman", "i love leetcode"\], \[5,3,2,2\]\)  
The system have already tracked down the following sentences and their corresponding times:  
`"i love you"`:`5`times  
`"island"`:`3`times  
`"ironman"`:`2`times  
`"i love leetcode"`:`2`times  
Now, the user begins another search:  
  
**Operation:**input\('i'\)  
**Output:**\["i love you", "island","i love leetcode"\]  
**Explanation:**  
There are four sentences that have prefix`"i"`. Among them, "ironman" and "i love leetcode" have same hot degree. Since`' '`has ASCII code 32 and`'r'`has ASCII code 114, "i love leetcode" should be in front of "ironman". Also we only need to output top 3 hot sentences, so "ironman" will be ignored.  
  
**Operation:**input\(' '\)  
**Output:**\["i love you","i love leetcode"\]  
**Explanation:**  
There are only two sentences that have prefix`"i "`.  
  
**Operation:**input\('a'\)  
**Output:**\[\]  
**Explanation:**  
There are no sentences that have prefix`"i a"`.  
  
**Operation:**input\('\#'\)  
**Output:**\[\]  
**Explanation:**  
The user finished the input, the sentence`"i a"`should be saved as a historical sentence in system. And the following input will be counted as a new search.

**Note:**

1. The input sentence will always start with a letter and end with '\#', and only one blank space will exist between two words.
2. The number of **complete sentences **that to be searched won't exceed 100. The length of each sentence including those in the historical data won't exceed 100.
3. Please use double-quote instead of single-quote when you write test cases even for a character input.
4. Please remember to **RESET **your class variables declared in class AutocompleteSystem, as static/class variables are **persisted across multiple test cases**. Please see [here](https://leetcode.com/faq/#different-output) for more details.

## Solution {#solution}

#### Approach \#1 Brute Force {#approach-1-brute-force-time-limit-exceeded}

In this solution, we make use of a HashMapmapmapwhich stores entries in the form\(sentencei,timesi\)\(sentence​i​​,times​i​​\). Here,timesitimes​i​​refers to the number of times thesentenceisentence​i​​has been typed earlier.

`AutocompleteSystem`: We pick up each sentence fromsentencessentencesand their corresponding times from thetimestimes, and make their entries in themapmapappropriately.

`input(c)`: We make use of a current sentence tracker variable,cursencur​s​​en, which is used to store the sentence entered till now as the input. Forccas the current input, firstly, we append thiscctocursencur​s​​enand then iterate over all the keys ofmapmapto check if a key exists whose initial characters match withcursencur​s​​en. We add all such keys to alistlist. Then, we sort thislistlistas per our requirements, and obtain the first three values from thislistlist.

**Performance Analysis**

* `AutocompleteSystem()`takesO\(k∗l\)O\(k∗l\)time. This is because, putting an entry in a hashMap takesO\(1\)O\(1\)time. But, to create a hash value for a sentence of average lengthkk, it will be scanned atleast once. We need to putllsuch entries in themapmap.

* `input()`takesO\(n+mlog\(m\)\)O\(n+mlog\(m\)\)time. We need to iterate over the list of sentences, inmapmap, entered till now\(say with a countnn\), takingO\(n\)O\(n\)time, to populate thelistlistused for finding the hot sentences. Then, we need to sort thelistlistof lengthmm, takingO\(mlog\(m\)\)O\(mlog\(m\)\)time.

```
public class AutocompleteSystem {
    HashMap < String, Integer > [] arr;
    class Node {
        Node(String st, int t) {
            sentence = st;
            times = t;
        }
        String sentence;
        int times;
    }
    public AutocompleteSystem(String[] sentences, int[] times) {
        arr = new HashMap[26];
        for (int i = 0; i < 26; i++)
            arr[i] = new HashMap < String, Integer > ();
        for (int i = 0; i < sentences.length; i++)
            arr[sentences[i].charAt(0) - 'a'].put(sentences[i], times[i]);
    }
    String cur_sent = "";
    public List < String > input(char c) {
        List < String > res = new ArrayList < > ();
        if (c == '#') {
            arr[cur_sent.charAt(0) - 'a'].put(cur_sent, arr[cur_sent.charAt(0) - 'a'].getOrDefault(cur_sent, 0) + 1);
            cur_sent = "";
        } else {
            List < Node > list = new ArrayList < > ();
            cur_sent += c;
            for (String key: arr[cur_sent.charAt(0) - 'a'].keySet()) {
                if (key.indexOf(cur_sent) == 0) {
                    list.add(new Node(key, arr[cur_sent.charAt(0) - 'a'].get(key)));
                }
            }
            Collections.sort(list, (a, b) -> a.times == b.times ? a.sentence.compareTo(b.sentence) : b.times - a.times);
            for (int i = 0; i < Math.min(3, list.size()); i++)
                res.add(list.get(i).sentence);
        }
        return res;
    }
}
```

#### Approach \#2 Using One level Indexing {#approach-2-using-one-level-indexingaccepted}

This method is almost the same as that of the last approach except that instead of making use of simply a HashMap to store the sentences along with their number of occurences, we make use of a Two level HashMap.

Thus, we make use of an arrayarrarrof HashMapsEach element of this array,arrarr, is used to refer to one of the alphabets possible. Each element is a HashMap itself, which stores the sentences and their number of occurences similar to the last approach. e.g.arr\[0\]arr\[0\]is used to refer to a HashMap which stores the sentences starting with an 'a'.

The process of adding the data in`AutocompleteSystem`and retrieving the data remains the same as in the last approach, except the one level indexing usingarrarrwhich needs to be done prior to accessing the required HashMap.

**Performance Analysis**

* `AutocompleteSystem()`takesO\(k∗l+26\)O\(k∗l+26\)time. Putting an entry in a hashMap takesO\(1\)O\(1\)time. But, to create a hash value for a sentence of average lengthkk, it will be scanned atleast once. We need to putllsuch entries in themapmap.

* `input()`takesO\(s+mlog\(m\)\)O\(s+mlog\(m\)\)time. We need to iterate only over one hashmap corresponding to the sentences starting with the first character of the current sentence, to populate thelistlistfor finding the hot sentences. Here,ssrefers to the size of this corresponding hashmap. Then, we need to sort thelistlistof lengthmm, takingO\(mlog\(m\)\)O\(mlog\(m\)\)time.

```
public class AutocompleteSystem {
    HashMap < String, Integer > [] arr;
    class Node {
        Node(String st, int t) {
            sentence = st;
            times = t;
        }
        String sentence;
        int times;
    }
    public AutocompleteSystem(String[] sentences, int[] times) {
        arr = new HashMap[26];
        for (int i = 0; i < 26; i++)
            arr[i] = new HashMap < String, Integer > ();
        for (int i = 0; i < sentences.length; i++)
            arr[sentences[i].charAt(0) - 'a'].put(sentences[i], times[i]);
    }
    String cur_sent = "";
    public List < String > input(char c) {
        List < String > res = new ArrayList < > ();
        if (c == '#') {
            arr[cur_sent.charAt(0) - 'a'].put(cur_sent, arr[cur_sent.charAt(0) - 'a'].getOrDefault(cur_sent, 0) + 1);
            cur_sent = "";
        } else {
            List < Node > list = new ArrayList < > ();
            cur_sent += c;
            for (String key: arr[cur_sent.charAt(0) - 'a'].keySet()) {
                if (key.indexOf(cur_sent) == 0) {
                    list.add(new Node(key, arr[cur_sent.charAt(0) - 'a'].get(key)));
                }
            }
            Collections.sort(list, (a, b) -> a.times == b.times ? a.sentence.compareTo(b.sentence) : b.times - a.times);
            for (int i = 0; i < Math.min(3, list.size()); i++)
                res.add(list.get(i).sentence);
        }
        return res;
    }
}
```

#### Approach \#3 Using Trie {#approach-3-using-trieaccepted}

A Trie is a special data structure used to store strings that can be visualized like a tree. It consists of nodes and edges. Each node consists of at max 26 children and edges connect each parent node to its children. These 26 pointers are nothing but pointers for each of the 26 letters of the English alphabet A separate edge is maintained for every edge.

Strings are stored in a top to bottom manner on the basis of their prefix in a trie. All prefixes of length 1 are stored at until level 1, all prefixes of length 2 are sorted at until level 2 and so on.

A Trie data structure is very commonly used for representing the words stored in a dictionary. Each level represents one character of the word being formed. A word available in the dictionary can be read off from the Trie by starting from the root and going till the leaf.

By doing a small modification to this structure, we can also include an entry,timestimes, for the number of times the current word has been previously typed. This entry can be stored in the leaf node corresponding to the particular word.

Now, for implementing the`AutoComplete`function, we need to consider each character of the every word given insentencessentencesarray, and add an entry corresponding to each such character at one level of the trie. At the leaf node of every word, we can update thetimestimessection of the node with the corresponding number of times this word has been typed.

The following figure shows a trie structure for the words "A","to", "tea", "ted", "ten", "i", "in", and "inn", occuring 15, 7, 3, 4, 12, 11, 5 and 9 times respectively.

Similarly, to implement the`input(c)`function, for every input charactercc, we need to add this character to the word being formed currently, i.e. tocursentcur​s​​ent. Then, we need to traverse in the current trie till all the characters in the current word,cursentcur​s​​ent, have been exhausted.

From this point onwards, we traverse all the branches possible in the Trie, put the sentences/words formed by these branches to alistlistalong with their corresponding number of occurences, and find the best 3 out of them similar to the last approach. The following animation shows a typical illustration.

**Performance Analysis**

* `AutocompleteSystem()`takesO\(k∗l\)O\(k∗l\)time. We need to iterate overllsentences each of average lengthkk, to create the trie for the given set ofsentencessentences.

* `input()`takesO\(p+q+mlog\(m\)\)O\(p+q+mlog\(m\)\)time. Here,pprefers to the length of the sentence formed till now,cursencur​s​​en.qqrefers to the number of nodes in the trie considering the sentence formed till now as the root node. Again, we need to sort thelistlistof lengthmmindicating the options available for the hot sentences, which takesO\(mlog\(m\)\)O\(mlog\(m\)\)time.

```

public class AutocompleteSystem {
    class Node {
        Node(String st, int t) {
            sentence = st;
            times = t;
        }
        String sentence;
        int times;
    }
    class Trie {
        int times;
        Trie[] branches = new Trie[27];
    }
    public int int_(char c) {
        return c == ' ' ? 26 : c - 'a';
    }
    public void insert(Trie t, String s, int times) {
        for (int i = 0; i < s.length(); i++) {
            if (t.branches[int_(s.charAt(i))] == null)
                t.branches[int_(s.charAt(i))] = new Trie();
            t = t.branches[int_(s.charAt(i))];
        }
        t.times += times;
    }
    public List < Node > lookup(Trie t, String s) {
        List < Node > list = new ArrayList < > ();
        for (int i = 0; i < s.length(); i++) {
            if (t.branches[int_(s.charAt(i))] == null)
                return new ArrayList < Node > ();
            t = t.branches[int_(s.charAt(i))];
        }
        traverse(s, t, list);
        return list;
    }
    public void traverse(String s, Trie t, List < Node > list) {
        if (t.times > 0)
            list.add(new Node(s, t.times));
        for (char i = 'a'; i <= 'z'; i++) {
            if (t.branches[i - 'a'] != null)
                traverse(s + i, t.branches[i - 'a'], list);
        }
        if (t.branches[26] != null)
            traverse(s + ' ', t.branches[26], list);
    }
    Trie root;
    public AutocompleteSystem(String[] sentences, int[] times) {
        root = new Trie();
        for (int i = 0; i < sentences.length; i++) {
            insert(root, sentences[i], times[i]);
        }
    }
    String cur_sent = "";
    public List < String > input(char c) {
        List < String > res = new ArrayList < > ();
        if (c == '#') { 
            insert(root, cur_sent, 1);
            cur_sent = "";
        } else {
            cur_sent += c;
            List < Node > list = lookup(root, cur_sent);
            Collections.sort(list, (a, b) -> a.times == b.times ? a.sentence.compareTo(b.sentence) : b.times - a.times);
            for (int i = 0; i < Math.min(3, list.size()); i++)
                res.add(list.get(i).sentence);
        }
        return res;
    }
}       
```



