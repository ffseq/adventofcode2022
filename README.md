# adventofcode2022
My various solutions for Advent of Code 2022

## Day 1a
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
Solution ← ⌈´+´¨ 

Solution Parse data

```
