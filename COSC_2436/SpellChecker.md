```java
import java.util.*;  
  
/*  
 * post-program thought here: * I might have done too much? I'm again just not too sure how far you'd want us to * go with these programs. * * I'm proud of this though, very robust. */public class SpellChecker {  
    private final Set<String> dictionary;  
  
    // Phonetic substitutions (i had this generated so it would refrain from being 26-odd lines)  
    private static final Map<String, String> PHONETIC_MAP = Map.ofEntries(Map.entry("ph", "f"), Map.entry("f", "ph"), Map.entry("c", "k"), Map.entry("k", "c"), Map.entry("s", "z"), Map.entry("z", "s"), Map.entry("x", "ks"), Map.entry("q", "kw"), Map.entry("v", "w"));  
  
    // QWERTY keyboard adjacency map (i had this generated so it would refrain from being 26-odd lines)  
    private static final Map<Character, Set<Character>> KEYBOARD_MAP = Map.ofEntries(Map.entry('a', Set.of('q', 'w', 's', 'z')), Map.entry('b', Set.of('v', 'g', 'h', 'n')), Map.entry('c', Set.of('x', 'd', 'f', 'v')), Map.entry('d', Set.of('s', 'e', 'r', 'f', 'c', 'x')), Map.entry('e', Set.of('w', 's', 'd', 'r')), Map.entry('f', Set.of('d', 'r', 't', 'g', 'v', 'c')), Map.entry('g', Set.of('f', 't', 'y', 'h', 'b', 'v')), Map.entry('h', Set.of('g', 'y', 'u', 'j', 'n', 'b')), Map.entry('i', Set.of('u', 'j', 'k', 'o')), Map.entry('j', Set.of('h', 'u', 'i', 'k', 'n', 'm')), Map.entry('k', Set.of('j', 'i', 'o', 'l', 'm')), Map.entry('l', Set.of('k', 'o', 'p')), Map.entry('m', Set.of('n', 'j', 'k')), Map.entry('n', Set.of('b', 'h', 'j', 'm')), Map.entry('o', Set.of('i', 'k', 'l', 'p')), Map.entry('p', Set.of('o', 'l')), Map.entry('q', Set.of('w', 'a')), Map.entry('r', Set.of('e', 'd', 'f', 't')), Map.entry('s', Set.of('a', 'w', 'e', 'd', 'x', 'z')), Map.entry('t', Set.of('r', 'f', 'g', 'y')), Map.entry('u', Set.of('y', 'h', 'j', 'i')), Map.entry('v', Set.of('c', 'f', 'g', 'b')), Map.entry('w', Set.of('q', 'a', 's', 'e')), Map.entry('x', Set.of('z', 's', 'd', 'c')), Map.entry('y', Set.of('t', 'g', 'h', 'u')), Map.entry('z', Set.of('a', 's', 'x')));  
  
    public SpellChecker(Set<String> words) {  
        this.dictionary = new HashSet<>(words);  
    }  
  
    /**  
     * Compute edit distance between two strings.     * (heavily influenced by Levenshtein)     * The edit distance is the minimum number of single-character edits     * (insertions, deletions, or substitutions are really the only possible things)     * required to change one string into the other.     * This implementation also considers keyboard-adjacent substitutions     * as a potential single edit to integrate into algorithm.     */    private int editDistance(String a, String b) {  
        int[][] dp = new int[a.length() + 1][b.length() + 1]; // 2d array  
        for (int i = 0; i <= a.length(); i++)  
            dp[i][0] = i;  
        for (int j = 0; j <= b.length(); j++)  
            dp[0][j] = j;  
        // the above two loops set the edges of our 2d comparison array between both words  
  
        for (int i = 1; i <= a.length(); i++) {  
            for (int j = 1; j <= b.length(); j++) {  
                int cost = (a.charAt(i - 1) == b.charAt(j - 1)) ? 0 : 1; //how many steps away are we?  
  
                // keyboard proximity included in algorithm                char c1 = a.charAt(i - 1);  
                char c2 = b.charAt(j - 1);  
                if (c1 != c2 && KEYBOARD_MAP.getOrDefault(c1, Set.of()).contains(c2)) {  
                    cost = 1;  
                }  
  
                dp[i][j] = Math.min(Math.min(dp[i - 1][j] + 1,             // deletion  
                                             dp[i][j - 1] + 1),            // insertion  
                                             dp[i - 1][j - 1] + cost);     // subsitution  
            }  
        }  
  
        return dp[a.length()][b.length()];  
    }  
  
    /**  
     * Suggest words from the dictionary that are within maxDistance of the input.     */    public List<String> spellCheck(String s) {  
        List<String> suggestions = new ArrayList<>();  
  
        // exact match  
        if (dictionary.contains(s)) {  
            suggestions.add(s);  
            return suggestions;  
        }  
  
        int maxDistance = 1;  
        while (suggestions.isEmpty() && maxDistance <= s.length() - 1) {  
            String normalizedInput = applyPhoneticSubstitutions(s.toLowerCase());  
  
            for (String word : dictionary) {  
                String normalizedWord = applyPhoneticSubstitutions(word.toLowerCase());  
                if (editDistance(normalizedInput, normalizedWord) <= maxDistance) {  
                    suggestions.add(word);  
                }  
            }  
  
            maxDistance++;  
        }  
  
        return suggestions;  
    }  
  
  
    /**  
     * Apply simple phonetic substitutions to a word     */    private String applyPhoneticSubstitutions(String word) {  
        String result = word;  
        for (Map.Entry<String, String> entry : PHONETIC_MAP.entrySet()) {  
            result = result.replace(entry.getKey(), entry.getValue());  
        }  
        return result;  
    }  
  
    public static void main(String[] args) {  
        Set<String> words = Set.of("theological", "osteoporosis", "live", "friend", "jacket", "bullets", "dove", "rover", "beginning");  
        SpellChecker checker = new SpellChecker(words);  
  
        String[] tests = {"jacket", "heogloiolcai", "osteoposris", "liVEe", "frined", "ajkcket", "bulet", "deov", "Rpovr", "rtlyjsdkg", "dover", "e", "sneer"};  
        for (String test : tests) {  
            System.out.println(test + " -> " + checker.spellCheck(test));  
        }  
    }  
}
```