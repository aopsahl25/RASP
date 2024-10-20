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
Problem 4:
```
>> set example("ababcabab")
>> sorted = sort(tokens, tokens);
     s-op: sorted
         Example: sorted("ababcabab") = [a, a, a, a, b, b, b, b, c] (strings)
>> lastone = length-1;
     s-op: lastone
         Example: lastone("ababcabab") = [8]*9 (ints)
>> def maxseq(seq) {
..   return load_from_location(sorted, lastone);
..   }
     console function: maxseq(seq)
>> maxseq(tokens);
     s-op: out
         Example: out("ababcabab") = [c]*9 (strings)
```
Problem 6.1:
```
>> dollar_loc = select_from_first(tokens, "$");
     selector: dollar_loc
         Example:
                             h e l l o $          
                         h |           1          
                         e |           1          
                         l |           1          
                         l |           1          
                         o |           1          
                         $ |           1          
                           |           1          
                           |           1          
                           |           1          
                           |           1          
                           |           1      
>> pos_dollar = aggregate(dollar_loc, indices);
     s-op: pos_dollar
         Example: pos_dollar("hello$     ") = [5]*11 (ints)
>> def secondhalf(seq){
..   return aggregate(select(indices, pos_dollar+pos_dollar-indices, ==), seq, " ");
..   }
     console function: secondhalf(seq)
>> def reverse_ag(seq){
..   return seq if indices<=pos_dollar else secondhalf(seq);
..   }
     console function: reverse_ag(seq)
>> reverse_ag(tokens);
     s-op: out
         Example: out("hello$     ") = [h, e, l, l, o, $, o, l, l, e, h] (strings)
>> reverse_ag(tokens);
     s-op: out
         Example: out("hello$ ") = [h, e, l, l, o, $, o] (strings)
>> reverse_ag(tokens);
     s-op: out
         Example: out("hello$X") = [h, e, l, l, o, $, o] (strings)
>> reverse_ag(tokens);
     s-op: out
         Example: out("hello$XXXXXXXXXX") = [h, e, l, l, o, $, o, l, l, e, h,  ,  ,  ,  ,  ] (strings)
```
Problem 6.2:
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
Problem 7:
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
Problem 8: Write a function that returns the minimum value in the sequence repeated for every position. 
```
>> sorted = sort(tokens, tokens);
     s-op: sorted
         Example: sorted("ababcabab") = [a, a, a, a, b, b, b, b, c]
>> def minseq(seq) {
..   return load_from_location(sorted, 0);
..   }
     console function: minseq(seq)
>> minseq(tokens);
     s-op: out
         Example: out("ababcabab") = [a]*9 (strings)
```
