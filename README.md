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
