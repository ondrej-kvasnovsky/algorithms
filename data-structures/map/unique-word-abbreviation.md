# Unique Word Abbreviation

An abbreviation of a word follows the form &lt;first letter&gt;&lt;number&gt;&lt;last letter&gt;. Below are some examples of word abbreviations:

```
a) it                      --> it    (no abbreviation)

     1
     ↓
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
     ↓   ↓    ↓    ↓  ↓    
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
     ↓   ↓    ↓
d) l|ocalizatio|n          --> l10n
```

Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if nootherword from the dictionary has the same abbreviation.

**Example:**

```
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

Here is a solution that will work for some cases, but not for cake and cane, it would return true. 

```
class ValidWordAbbr {

    private Set<String> dictionary = new HashSet<>();
    
    public ValidWordAbbr(String[] dictionary) {
        for (String word : dictionary) {
            this.dictionary.add(abbreviate(word));
        }
        System.out.println(this.dictionary);
    }
    
    public boolean isUnique(String word) {
        return !dictionary.contains(abbreviate(word));
    }
    
    private String abbreviate(String word) {
        if (word.length() < 3) {
            return word;
        } 
        int length = word.length() ;
        return "" + word.charAt(0) + (length - 2) + word.charAt(length - 1);
    }
}

/**
 * Your ValidWordAbbr object will be instantiated and called as such:
 * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
 * boolean param_1 = obj.isUnique(word);
 */
```

That means, we need to create abbreviations and then put all words into a set which is referenced by that abbreviation. Something like this.

```
class ValidWordAbbr {

    private Map<String, Set<String>> dictionary = new HashMap<>();
    
    public ValidWordAbbr(String[] dictionary) {
        for (String word : dictionary) {
            String abr = abbreviate(word);
            Set<String> set = this.dictionary.getOrDefault(abr, new HashSet<>());
            set.add(word);
            this.dictionary.put(abr, set);
        }
    }
    
    public boolean isUnique(String word) {
        String abr = abbreviate(word);
        if (!dictionary.containsKey(abr)) {
            return true;
        }
        return dictionary.get(abr).contains(word) && dictionary.get(abr).size() == 1;
    }
    
    private String abbreviate(String word) {
        if (word.length() < 3) {
            return word;
        } 
        int length = word.length() ;
        return "" + word.charAt(0) + (length - 2) + word.charAt(length - 1);
    }
}
```



