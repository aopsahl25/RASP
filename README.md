# RASP HOMEWORK 03

Problem 1:
```
>> def reverse_function(seq) {
          return aggregate(select(indices, length-indices-1, ==), seq);
      }
      console function: reverse_function(seq)
>> reverse = reverse_function(indices);
  s-op: reverse
         Example: reverse("hello") = [4, 3, 2, 1, 0] (ints)
>> reverse("hello"):
      =  [4, 3, 2, 1, 0] (ints)
```
Problem 2:
```
>> def rotate(seq, count) {
..    return aggregate(select(indices, indices-count, ==), seq, "x") if count<=indices else aggregate(select(indices, indices+length-count, ==), seq, "x");
..   }
     console function: rotate(seq, count)
>> rotate(tokens, 0);
     s-op: out
         Example: out("hello") = [h, e, l, l, o] (strings)
>> rotate(tokens, 1);
     s-op: out
         Example: out("hello") = [o, h, e, l, l] (strings)
>> rotate(tokens, 2);
     s-op: out
         Example: out("hello") = [l, o, h, e, l] (strings)
```
Problem 3:
```
>> def swap(seq){
..   return aggregate(select(indices, indices+1, ==), tokens, "x") if indices%2==0 else aggregate(select(indices, indices-1, ==), tokens, "x"); 
..   }
>> def newswap(seq){
..   return aggregate(select(indices, indices, ==), tokens, "x") if indices==length-1 and length%2==1 else swap(seq);
..   }
>> set example("hello")
>> newswap(tokens);
     s-op: out
         Example: out("hello") = [e, h, l, l, o] (strings)
>> set example("ababab")
>> newswap(tokens);
     s-op: out
         Example: out("ababab") = [b, a, b, a, b, a] (strings)
```
Problem 6.2
```
>> def howmany(seq, atom){
..   return selector_width(select(seq, atom, ==)) if contains(seq, atom) else "0";
..   }
>> set example("hello")
>> howmany(tokens, "a");
     s-op: out
         Example: out("hello") = [0]*5 (strings)
>> howmany(tokens, "h");
     s-op: out
         Example: out("hello") = [1]*5 (ints)
>> howmany(tokens, "l");
     s-op: out
         Example: out("hello") = [2]*5 (ints)
```
Problem 7
```
>> one = indices+1
>> def ag_count(seq, atom){
..   return round(one*aggregate(mask_ag, indicator(seq==atom))) if contains(seq, atom) else "0";
..   }
     console function: ag_count(seq, atom)
>> ag_count(tokens, "a");
     s-op: out
         Example: out("hello") = [0]*5 (strings)
>> ag_count(tokens, "h");
     s-op: out
         Example: out("hello") = [1]*5 (ints)
>> ag_count(tokens, "e");
     s-op: out
         Example: out("hello") = [0, 1, 1, 1, 1] (ints)
>> ag_count(tokens, "l");
     s-op: out
         Example: out("hello") = [0, 0, 1, 2, 2] (ints)
```
