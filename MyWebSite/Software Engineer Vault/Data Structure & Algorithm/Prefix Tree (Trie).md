---
Created: 2023-04-09 13:41
alias: [prefix tree, trie]
---
## Description
---

Prefix tree is a type of k-array tree, as a tree stored more than two leafs in the same time. It is used commonly in auto-complete, word search system.

The following is basic Go implementation

```go
type Trie struct {
	IsWord  bool
	TrieMap map[byte]*Trie
}

func Construct() Trie {
	return Trie{
		IsWord:  false,
		TrieMap: make(map[byte]*Trie),
	}
}

func (trie *Trie) Add(node *Trie, word *string, index int) {
	if index == len(*word) {
		node.IsWord = true
		return
	}

	char := (*word)[index]
	if ptrTrie, ok := node.TrieMap[char]; ok {
		trie.Add(ptrTrie, word, index+1)
	} else {
		t := Construct()
		node.TrieMap[char] = &t
		trie.Add(&t, word, index+1)
	}
}

func (trie *Trie) Search(node *Trie, word *string, index int) bool {
	if index == len(*word) {
		return node.IsWord
	}

	char := (*word)[index]
	if ptrTrie, ok := node.TrieMap[char]; ok {
		return trie.Search(ptrTrie, word, index+1)
	}
	return false
}
```