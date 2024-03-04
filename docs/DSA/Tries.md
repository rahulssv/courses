# Tries

### [Implement Trie Prefix Tree](https://leetcode.com/problems/implement-trie-prefix-tree/)

```java
class TrieNode{
    boolean isWord;
    TrieNode[] children;
    public TrieNode(){
        isWord=false;
        children=new TrieNode[26];
    }
}
class Trie {
    TrieNode root;
    public Trie() {
        root=new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode node=root;
        for(char c:word.toCharArray()){
            int index=c-'a';
            if(node.children[index]==null){
                node.children[index]=new TrieNode();
            }
            node=node.children[index];
        }
        node.isWord=true;
    }
    
    public boolean search(String word) {
        TrieNode node=root;
        for(char c:word.toCharArray()){
            int index=c-'a';
            if(node.children[index]==null){
                return false;
            }
            node=node.children[index];
        }
        return node.isWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node=root;
        for(char c:prefix.toCharArray()){
            int index=c-'a';
            if(node.children[index]==null){
                return false;
            }
            node=node.children[index];
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

### [Design Add And Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

```java
class WordDictionary {
    boolean isWord;
    WordDictionary[] children;
    public WordDictionary() {
        isWord=false;
        children=new WordDictionary[26];
    }
    
    public void addWord(String word) {
        WordDictionary node=this;
        for(char c:word.toCharArray()){
            int index=c-'a';
            
            if(node.children[index]==null){
                node.children[index]=new WordDictionary();
            }
            node=node.children[index];
        }
        node.isWord=true;
    }
    
    public boolean search(String word) {
        WordDictionary node=this;
        for(int i=0;i<word.length();i++){
            char c=word.charAt(i);
            if(c=='.'){
                for(WordDictionary child:node.children){
                    if(child!=null){
                        
                        if(child.search( word.substring(i+1))){
                            return true;
                        }
                    } 
                }
                return false;
            }else{
               int index=c-'a'; 
               if(node.children[index]==null){
                    return false;
                }
                node=node.children[index];
            }
        }
        
        return node!=null&&node.isWord;
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

### [Word Search II](https://leetcode.com/problems/word-search-ii/)

```java
class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<String>();
        Trie root = buildTrie(words);
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                dfs(board, i, j, root, res);
            }
        }
        return res;

    }

    private void dfs(char[][] board, int i, int j, Trie root, List<String> res) {
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] == '#'
                || root.children[board[i][j] - 'a'] == null)
            return;
        char c = board[i][j];
        root = root.children[c - 'a'];
        if (root.word != null) {
            res.add(root.word);
            root.word = null;
        }
        board[i][j] = '#';
        dfs(board, i - 1, j, root, res);
        dfs(board, i + 1, j, root, res);
        dfs(board, i, j - 1, root, res);
        dfs(board, i, j + 1, root, res);
        board[i][j] = c;
    }

    private Trie buildTrie(String[] words) {
        Trie root = new Trie();
        for (String word : words) {
            Trie temp = root;
            for (char c : word.toCharArray()) {
                int index = c - 'a';
                if (temp.children[index] == null) {
                    temp.children[index] = new Trie();
                }
                temp = temp.children[index];
            }
            temp.word = word;
        }
        return root;

    }
}

class Trie {
    Trie[] children = new Trie[26];
    String word;
}
```