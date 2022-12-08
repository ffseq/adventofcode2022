# adventofcode2022
My various solutions for Advent of Code 2022

## Day 1
```apl
# Utils from BQNcrate
Split ← ((⊢-˜+`×¬)∘=⊔⊢)
ToNum ← (10⊸×⊸+˜´∘⌽-⟜'0')

# Sample data
data ← "1000
2000
3000

4000

5000
6000

7000
8000
9000

10000"

# Parsing is the hard part
Parse ← {
  # Prepending newline makes things easier later
  data ← ⟨@+10⟩∾𝕩
  # Each blank line looks like two 1's on a 2 window equals mask
  # "Find" these 1 1 windows, deshape
  # The window function reduces length by one, joining a 0 corrects for this...
  # ...so we can do a plus scan
  mask ← +` 0∾ ⥊ 1‿1⍷ 2↕ (@+10)=data
  # Group using mask, split on each subarray by newline, then drop the first empty list in each subarray
  # And convert to decimal from string with ToNum on depth 1
  ToNum⚇1 1↓¨(@+10)Split¨ mask⊔data
}

# Solution itself is cake
SolutionPart1 ← ⌈´+´¨ 

•Show SolutionPart1 Parse data

SolutionPart2 ← {+´3↑⌽∧+´¨𝕩}

SolutionPart2 Parse data

```

## Day 2
```apl

input ← "A Y
B X
C Z
"
input ↩ (@+10) Split input

# Trick is realizing all 9 possible combos map 1-1 with integers 1-9,
# so we can use indexing in a simple list + 1
Score ← ⊑1+⟨
"B X"
"C Y"
"A Z"
"A X"
"B Y"
"C Z"
"C X"
"A Y"
"B Z"
⟩⊐<

# Part 1
+´ Score¨ input

# Part 2 is identical, just a different mapping
Score ← ⊑1+⟨
"B X"
"C X"
"A X"
"A Y"
"B Y"
"C Y"
"C Z"
"A Z"
"B Z"
⟩⊐<

+´ Score¨ input

```
