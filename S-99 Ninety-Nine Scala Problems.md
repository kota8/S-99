
Problem site: [http://aperiodic.net/phil/scala/s-99/](http://aperiodic.net/phil/scala/s-99/)


### P01 (*) Find the last element of a list.
  
Example:

```scala
scala> last(List(1, 1, 2, 3, 5, 8))
res0: Int = 8
```


```scala211
def last[T](x: List[T]): T = x match {
  case Nil      => throw new NoSuchElementException("last(Nil)")
  case a :: Nil => a
  case a :: as  => last(as)
}

last(List(1, 1, 2, 3, 5, 8))
```




    defined [32mfunction[39m [36mlast[39m
    [36mres1_1[39m: [32mInt[39m = [32m8[39m



### P02 (*) Find the last but one element of a list.

Example:

```scala
scala> penultimate(List(1, 1, 2, 3, 5, 8))
res0: Int = 5
```


```scala211
def penultimate[T](x: List[T]): T = x match {
  case Nil | _ :: Nil  => throw new NoSuchElementException("penultimate with list shorter than 2")
  case a1 :: a2 :: Nil => a1
  case a :: as         => penultimate(as)
}

penultimate(List(1, 1, 2, 3, 5, 8))
```




    defined [32mfunction[39m [36mpenultimate[39m
    [36mres2_1[39m: [32mInt[39m = [32m5[39m



### P03 (*) Find the Kth element of a list.

By convention, the first element in the list is element 0.

Example:

```scala
scala> nth(2, List(1, 1, 2, 3, 5, 8))
res0: Int = 2
```


```scala211
def nth[T](i: Int, x: List[T]): T = {
  if (x.length < i) throw new NoSuchElementException("x is shorter than i")
  if (i < 0) throw new NoSuchElementException("i is negative")
  else if (i == 0) x.head
  else nth(i-1, x.tail)
}

nth(2, List(1, 1, 2, 3, 5, 8))
```




    defined [32mfunction[39m [36mnth[39m
    [36mres3_1[39m: [32mInt[39m = [32m2[39m



### P04 (*) Find the number of elements of a list.

Example:

```scala
scala> length(List(1, 1, 2, 3, 5, 8))
res0: Int = 6
```


```scala211
def length[T](x: List[T]): Int = {
  def loop(acc: Int, y: List[T]): Int = y match {
    case Nil      => acc
    case a :: as  => loop(acc+1, as)    
  }
  loop(0, x)
}

length(List(1, 1, 2, 3, 5, 8))
length(Nil)
length(List(8))
```




    defined [32mfunction[39m [36mlength[39m
    [36mres4_1[39m: [32mInt[39m = [32m6[39m
    [36mres4_2[39m: [32mInt[39m = [32m0[39m
    [36mres4_3[39m: [32mInt[39m = [32m1[39m



### P05 (*) Reverse a list.

Example:

```scala
scala> reverse(List(1, 1, 2, 3, 5, 8))
res0: List[Int] = List(8, 5, 3, 2, 1, 1)
```


```scala211
def reverse[T](x: List[T]): List[T] = {
  def loop(acc: List[T], y: List[T]): List[T] = y match {
    case Nil  => acc
    case a :: as => loop(a :: acc, as)
  }
  loop(Nil, x)
}

reverse(List(1, 1, 2, 3, 5, 8))
```




    defined [32mfunction[39m [36mreverse[39m
    [36mres5_1[39m: [32mList[39m[[32mInt[39m] = [33mList[39m([32m8[39m, [32m5[39m, [32m3[39m, [32m2[39m, [32m1[39m, [32m1[39m)



### P06 (*) Find out whether a list is a palindrome.

Example:

```scala
scala> isPalindrome(List(1, 2, 3, 2, 1))
res0: Boolean = true
```


```scala211
def isPalindrome[T](x: List[T]): Boolean = {
  def helper(l1: List[T], l2: List[T]): Boolean = {
    if (l1.length==0) true
    else if (l1.length == l2.length) {
      if (l1.head == l2.head) helper(l1.tail, l2.tail) else false
    }
    else if (l1.length == l2.length+1) helper(l1.tail, l2)
    else helper(l1.tail, l1.head :: l2)
  }
  helper(x, Nil)
}

isPalindrome(List(1, 2, 3, 2, 1))
isPalindrome(List(1, 2, 2, 1))
isPalindrome(List(1, 3, 2, 1))
isPalindrome(List(10, 10))
isPalindrome(List(99))
isPalindrome(List(5, 4))
```




    defined [32mfunction[39m [36misPalindrome[39m
    [36mres6_1[39m: [32mBoolean[39m = [32mtrue[39m
    [36mres6_2[39m: [32mBoolean[39m = [32mtrue[39m
    [36mres6_3[39m: [32mBoolean[39m = [32mfalse[39m
    [36mres6_4[39m: [32mBoolean[39m = [32mtrue[39m
    [36mres6_5[39m: [32mBoolean[39m = [32mtrue[39m
    [36mres6_6[39m: [32mBoolean[39m = [32mfalse[39m



### P07 (**) Flatten a nested list structure.
    
Example:

```scala
scala> flatten(List(List(1, 1), 2, List(3, List(5, 8))))
res0: List[Any] = List(1, 1, 2, 3, 5, 8)
```


```scala211
def flatten(x: List[Any]): List[Any] = { 
  x match {
    case Nil                => Nil       
    case (a: List[_]) :: as => flatten(a) ::: flatten(as)  
    case a :: as            => a :: flatten(as)  
  } 
}
flatten(List(List(1, 1), 2, List(3, List(5, 8))))
```




    defined [32mfunction[39m [36mflatten[39m
    [36mres7_1[39m: [32mList[39m[[32mAny[39m] = [33mList[39m(1, 1, 2, 3, 5, 8)



### P08 (**) Eliminate consecutive duplicates of list elements.

If a list contains repeated elements they should be replaced with a single copy of the element. 
The order of the elements should not be changed.

Example:

```scala
scala> compress(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
res0: List[Symbol] = List('a, 'b, 'c, 'a, 'd, 'e)
```


```scala211
def compress[T](x: List[T]): List[T] = {
  def inner(acc: List[T], y: List[T]): List[T] = {
    y match {
      case Nil      => acc
      case a :: Nil => a :: acc 
      case a :: as  => if (a==as.head) inner(acc, as) else inner(a::acc, as)
    }  
  }
  inner(Nil, x).reverse
/*  x match {
    case Nil => Nil
    case a :: Nil => a :: Nil
    case a :: as => if (a==as.head) compress(as) else a :: compress(as)
  }
  */
}
compress(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
```




    defined [32mfunction[39m [36mcompress[39m
    [36mres8_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'a[39m, [32m'd[39m, [32m'e[39m)



### P09 (**) Pack consecutive duplicates of list elements into sublists.

If a list contains repeated elements they should be placed in separate sublists.

Example:

```scala
scala> pack(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
res0: List[List[Symbol]] = List(List('a, 'a, 'a, 'a), List('b), List('c, 'c), List('a, 'a), List('d), List('e, 'e, 'e, 'e))
```


```scala211
def pack[T](x: List[T]): List[List[T]] = {
  def inner(acc: List[List[T]], cur: T, curAcc: List[T], y: List[T]): List[List[T]] = {
    y match {
      case Nil => curAcc::acc
      case a :: as => {
        if (a == cur) inner(acc, cur, a::curAcc, as) 
        else          inner(curAcc::acc, a, List(a), as)
      }
    }  
  }
  x match {
    case Nil => Nil
    case a::as => inner(Nil, a, List(a), as).reverse
  }
}
pack(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
```




    defined [32mfunction[39m [36mpack[39m
    [36mres9_1[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'a[39m, [32m'a[39m, [32m'a[39m, [32m'a[39m),
      [33mList[39m([32m'b[39m),
      [33mList[39m([32m'c[39m, [32m'c[39m),
      [33mList[39m([32m'a[39m, [32m'a[39m),
      [33mList[39m([32m'd[39m),
      [33mList[39m([32m'e[39m, [32m'e[39m, [32m'e[39m, [32m'e[39m)
    )



### P10 (*) Run-length encoding of a list.

Use the result of problem P09 to implement the so-called run-length encoding data compression method. Consecutive duplicates of elements are encoded as tuples (N, E) where N is the number of duplicates of the element E.

Example:

```scala
scala> encode(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
res0: List[(Int, Symbol)] = List((4,'a), (1,'b), (2,'c), (2,'a), (1,'d), (4,'e))
```


```scala211
def encode[T](x: List[T]): List[(Int, T)] = {
  pack(x) map { y: List[T] => (y.length, y.head) }
}
encode(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
```




    defined [32mfunction[39m [36mencode[39m
    [36mres10_1[39m: [32mList[39m[([32mInt[39m, [32mSymbol[39m)] = [33mList[39m(([32m4[39m, [32m'a[39m), ([32m1[39m, [32m'b[39m), ([32m2[39m, [32m'c[39m), ([32m2[39m, [32m'a[39m), ([32m1[39m, [32m'd[39m), ([32m4[39m, [32m'e[39m))



### P11 (*) Modified run-length encoding.
    
Modify the result of problem P10 in such a way that if an element has no duplicates it is simply copied into the result list. Only elements with duplicates are transferred as (N, E) terms. 

Example:

```scala
scala> encodeModified(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
res0: List[Any] = List((4,'a), 'b, (2,'c), (2,'a), 'd, (4,'e))
```


```scala211
def encodeModified[T](x: List[T]): List[Any] = {
  pack(x) map { y: List[T] => if (y.length==1) y.head else (y.length, y.head) }
}
encodeModified(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
```




    defined [32mfunction[39m [36mencodeModified[39m
    [36mres11_1[39m: [32mList[39m[[32mAny[39m] = [33mList[39m((4,'a), 'b, (2,'c), (2,'a), 'd, (4,'e))



### P12 (**) Decode a run-length encoded list.

Given a run-length code list generated as specified in problem P10, construct its uncompressed version.

Example:

```scala
scala> decode(List((4, 'a), (1, 'b), (2, 'c), (2, 'a), (1, 'd), (4, 'e)))
res0: List[Symbol] = List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e)
```


```scala211
def decode[T](x: List[(Int, T)]) = {
// x flatMap { y: (Int, T) => (1 to y._1) map { Int => y._2 } }  
  x flatMap { y: (Int, T) => List.fill(y._1)(y._2) }  
}
decode(List((4, 'a), (1, 'b), (2, 'c), (2, 'a), (1, 'd), (4, 'e)))
```




    defined [32mfunction[39m [36mdecode[39m
    [36mres12_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'a[39m, [32m'a[39m, [32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'c[39m, [32m'a[39m, [32m'a[39m, [32m'd[39m, [32m'e[39m, [32m'e[39m, [32m'e[39m, [32m'e[39m)



### P13 (**) Run-length encoding of a list (direct solution).

Implement the so-called run-length encoding data compression method directly. I.e. don't use other methods you've written (like P09's pack); do all the work directly.

Example:

```scala
scala> encodeDirect(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
res0: List[(Int, Symbol)] = List((4,'a), (1,'b), (2,'c), (2,'a), (1,'d), (4,'e))
```


```scala211
def encodeDirect[T](x: List[T]): List[(Int, T)] = {
  def inner(acc: List[(Int, T)], cur: T, curCount: Int, y: List[T]): List[(Int, T)] = {
    y match {
      case Nil     => (curCount, cur) :: acc
      case a :: as => {
        if (a == cur) inner(acc, cur, curCount+1, as) 
        else          inner((curCount, cur) :: acc, a, 1, as)
      }
    }  
  }
  x match {
    case Nil     => Nil
    case a :: as => inner(Nil, a, 1, as).reverse
  }
}
encodeDirect(List('a, 'a, 'a, 'a, 'b, 'c, 'c, 'a, 'a, 'd, 'e, 'e, 'e, 'e))
```




    defined [32mfunction[39m [36mencodeDirect[39m
    [36mres13_1[39m: [32mList[39m[([32mInt[39m, [32mSymbol[39m)] = [33mList[39m(([32m4[39m, [32m'a[39m), ([32m1[39m, [32m'b[39m), ([32m2[39m, [32m'c[39m), ([32m2[39m, [32m'a[39m), ([32m1[39m, [32m'd[39m), ([32m4[39m, [32m'e[39m))



### P14 (*) Duplicate the elements of a list.

Example:

```scala
scala> duplicate(List('a, 'b, 'c, 'c, 'd))
res0: List[Symbol] = List('a, 'a, 'b, 'b, 'c, 'c, 'c, 'c, 'd, 'd)
```


```scala211
def duplicate[T](x: List[T]): List[T] = {
  x flatMap { y: T => List.fill(2)(y) }  
}
duplicate(List('a, 'b, 'c, 'c, 'd))
```




    defined [32mfunction[39m [36mduplicate[39m
    [36mres14_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'a[39m, [32m'b[39m, [32m'b[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'd[39m, [32m'd[39m)



### P15 (**) Duplicate the elements of a list a given number of times.

Example:

```scala
scala> duplicateN(3, List('a, 'b, 'c, 'c, 'd))
res0: List[Symbol] = List('a, 'a, 'a, 'b, 'b, 'b, 'c, 'c, 'c, 'c, 'c, 'c, 'd, 'd, 'd)
```


```scala211
def duplicateN[T](n: Int, x: List[T]): List[T] = {
  x flatMap { y: T => List.fill(n)(y) }  
}
duplicateN(3, List('a, 'b, 'c, 'c, 'd))
```




    defined [32mfunction[39m [36mduplicateN[39m
    [36mres15_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'a[39m, [32m'a[39m, [32m'b[39m, [32m'b[39m, [32m'b[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'c[39m, [32m'd[39m, [32m'd[39m, [32m'd[39m)



### P16 (**) Drop every Nth element from a list.

Example:

```scala
scala> drop(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
res0: List[Symbol] = List('a, 'b, 'd, 'e, 'g, 'h, 'j, 'k)
```


```scala211
def drop[T](i: Int, x: List[T]): List[T] = {
  def inner(acc: List[T], y: List[T], cur: Int): List[T] = {
    y match {
      case Nil     => acc
      case a :: as => {
        if (cur % i == 0) inner(acc, as, 1) 
        else              inner(a :: acc, as, cur+1)
      }
    }
  }
  inner(Nil, x, 1).reverse
}
drop(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
```




    defined [32mfunction[39m [36mdrop[39m
    [36mres16_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'b[39m, [32m'd[39m, [32m'e[39m, [32m'g[39m, [32m'h[39m, [32m'j[39m, [32m'k[39m)



### P17 (*) Split a list into two parts.

The length of the first part is given. Use a Tuple for your result.

Example:

```scala
scala> split(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
res0: (List[Symbol], List[Symbol]) = (List('a, 'b, 'c),List('d, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
```


```scala211
def split[T](i: Int, x: List[T]): (List[T], List[T]) = {
  def inner(j: Int, o1: List[T], o2: List[T]): (List[T], List[T]) = {
    if (j <= 0) (o1.reverse, o2)
    else {
      o2 match {
        case Nil => throw new IndexOutOfBoundsException()
        case a :: as => inner(j-1, a :: o1, as)
      }
    }
  }
  inner(i, Nil, x)
}
split(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
split(0, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
split(11, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
//split(12, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))  // error case
```




    defined [32mfunction[39m [36msplit[39m
    [36mres17_1[39m: ([32mList[39m[[32mSymbol[39m], [32mList[39m[[32mSymbol[39m]) = ([33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m), [33mList[39m([32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m))
    [36mres17_2[39m: ([32mList[39m[[32mSymbol[39m], [32mList[39m[[32mSymbol[39m]) = ([33mList[39m(), [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m))
    [36mres17_3[39m: ([32mList[39m[[32mSymbol[39m], [32mList[39m[[32mSymbol[39m]) = ([33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m), [33mList[39m())



### P18 (**) Extract a slice from a list.

Given two indices, I and K, the slice is the list containing the elements from and including the Ith element up to but not including the Kth element of the original list. Start counting the elements with 0.

Example:

```scala
scala> slice(3, 7, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
res0: List[Symbol] = List('d, 'e, 'f, 'g)
```


```scala211
def slice[T](i: Int, j: Int, x: List[T]): List[T] = {
  def helper(k: Int, y: List[T]): List[T] = if (k <= 0) y else helper(k-1, y.tail)
  // `helper` returns y[k:]  
  helper(i, x).take(j-i)  
}
slice(3, 7, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
```




    defined [32mfunction[39m [36mslice[39m
    [36mres18_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m)



### P19 (**) Rotate a list N places to the left.

Examples:

```scala
scala> rotate(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
res0: List[Symbol] = List('d, 'e, 'f, 'g, 'h, 'i, 'j, 'k, 'a, 'b, 'c)
```
```scala
scala> rotate(-2, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
res1: List[Symbol] = List('j, 'k, 'a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i)
```


```scala211
def rotate[T](i: Int, x: List[T]): List[T] = {
  lazy val n = x.length
  val j = if (i >= 0) i else n + i
  assert(j >= 0 && j <= n)
  def inner(k: Int, o1: List[T], o2: List[T]): List[T] = {
    if (k <= 0) o1 ++ o2.reverse 
    else        inner(k-1, o1.tail, o1.head :: o2)
  }
  inner(j, x, Nil)
}
rotate(3, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
rotate(-2, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
//rotate(12, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))   // error
rotate(11, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
rotate(0, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
rotate(-11, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))
//rotate(-12, List('a, 'b, 'c, 'd, 'e, 'f, 'g, 'h, 'i, 'j, 'k))  // error

```




    defined [32mfunction[39m [36mrotate[39m
    [36mres19_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m, [32m'a[39m, [32m'b[39m, [32m'c[39m)
    [36mres19_2[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'j[39m, [32m'k[39m, [32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m)
    [36mres19_3[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m)
    [36mres19_4[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m)
    [36mres19_5[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m, [32m'g[39m, [32m'h[39m, [32m'i[39m, [32m'j[39m, [32m'k[39m)



### P20 (*) Remove the Kth element from a list.

Return the list and the removed element in a Tuple. Elements are numbered from 0.

Example:

```scala
scala> removeAt(1, List('a, 'b, 'c, 'd))
res0: (List[Symbol], Symbol) = (List('a, 'c, 'd),'b)
```


```scala211
def removeAt[T](i: Int, x: List[T]): (List[T], T) = {
  def inner(j: Int, o1: List[T], o2: List[T]): (List[T], T) = {
    if (j==0) (o1.reverse ++ o2.tail, o2.head) 
    else      inner(j-1, o2.head :: o1, o2.tail)
  }
  inner(i, Nil, x)  
}
removeAt(1, List('a, 'b, 'c, 'd))
removeAt(0, List('a, 'b, 'c, 'd))
removeAt(3, List('a, 'b, 'c, 'd))
//removeAt(4, List('a, 'b, 'c, 'd))   // error
```




    defined [32mfunction[39m [36mremoveAt[39m
    [36mres20_1[39m: ([32mList[39m[[32mSymbol[39m], [32mSymbol[39m) = ([33mList[39m([32m'a[39m, [32m'c[39m, [32m'd[39m), [32m'b[39m)
    [36mres20_2[39m: ([32mList[39m[[32mSymbol[39m], [32mSymbol[39m) = ([33mList[39m([32m'b[39m, [32m'c[39m, [32m'd[39m), [32m'a[39m)
    [36mres20_3[39m: ([32mList[39m[[32mSymbol[39m], [32mSymbol[39m) = ([33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m), [32m'd[39m)



### P21 (*) Insert an element at a given position into a list.

Example:

```scala
scala> insertAt('new, 1, List('a, 'b, 'c, 'd))
res0: List[Symbol] = List('a, 'new, 'b, 'c, 'd)
```


```scala211
def insertAt[T](elem: T, i: Int, x: List[T]): List[T] = {
  def inner(j: Int, o1: List[T], o2: List[T]): List[T] = {
    if (j==0) o1.reverse ++ (elem :: o2)
    else      inner(j-1, o2.head :: o1, o2.tail)
  }
  inner(i, Nil, x)
}
insertAt('new, 1, List('a, 'b, 'c, 'd))
```




    defined [32mfunction[39m [36minsertAt[39m
    [36mres21_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'a[39m, [32m'new[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m)



### P22 (*) Create a list containing all integers within a given range.

Example:

```scala
scala> range(4, 9)
res0: List[Int] = List(4, 5, 6, 7, 8, 9)
```


```scala211
def range(i: Int, j: Int): List[Int] = (i to j).toList
range(4, 9)
```




    defined [32mfunction[39m [36mrange[39m
    [36mres22_1[39m: [32mList[39m[[32mInt[39m] = [33mList[39m([32m4[39m, [32m5[39m, [32m6[39m, [32m7[39m, [32m8[39m, [32m9[39m)



### P23 (**) Extract a given number of randomly selected elements from a list.

Example:

```scala
scala> randomSelect(3, List('a, 'b, 'c, 'd, 'f, 'g, 'h))
res0: List[Symbol] = List('e, 'd, 'a)
```

Hint: Use the solution to problem P20


```scala211
def randomSelect[T](n: Int, x: List[T]): List[T] = {
  val rnd = scala.util.Random
  def inner(acc: List[T], y: List[T], ysize:Int, m: Int): List[T] = {    
    if (m==0) acc
    else {
      val tmp = removeAt(rnd.nextInt(ysize), y)
      inner(tmp._2 :: acc, tmp._1, ysize-1, m-1)
    }
  }
  inner(Nil, x, x.length, n)
}
randomSelect(3, List('a, 'b, 'c, 'd, 'f, 'g, 'h))
```




    defined [32mfunction[39m [36mrandomSelect[39m
    [36mres23_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'h[39m, [32m'c[39m, [32m'g[39m)



### P24 (*) Lotto: Draw N different random numbers from the set 1..M.

Example:

```scala
scala> lotto(6, 49)
res0: List[Int] = List(23, 1, 17, 33, 21, 37)
```


```scala211
def lotto(n: Int, m: Int): List[Int] = randomSelect(n, (1 to m).toList)
lotto(6, 49)
```




    defined [32mfunction[39m [36mlotto[39m
    [36mres24_1[39m: [32mList[39m[[32mInt[39m] = [33mList[39m([32m26[39m, [32m14[39m, [32m28[39m, [32m13[39m, [32m15[39m, [32m42[39m)



### P25 (*) Generate a random permutation of the elements of a list.

Hint: Use the solution of problem P23.

Example:

```scala
scala> randomPermute(List('a, 'b, 'c, 'd, 'e, 'f))
res0: List[Symbol] = List('b, 'a, 'd, 'c, 'e, 'f)
```


```scala211
def randomPermute[T](x: List[T]): List[T] = randomSelect(x.length, x)
randomPermute(List('a, 'b, 'c, 'd, 'e, 'f))
```




    defined [32mfunction[39m [36mrandomPermute[39m
    [36mres25_1[39m: [32mList[39m[[32mSymbol[39m] = [33mList[39m([32m'c[39m, [32m'f[39m, [32m'd[39m, [32m'e[39m, [32m'b[39m, [32m'a[39m)



### P26 (**) Generate the combinations of K distinct objects chosen from the N elements of a list.

In how many ways can a committee of 3 be chosen from a group of 12 people? We all know that there are C(12,3) = 220 possibilities (C(N,K) denotes the well-known binomial coefficient). For pure mathematicians, this result may be great. But we want to really generate all the possibilities.

Example:

```scala
scala> combinations(3, List('a, 'b, 'c, 'd, 'e, 'f))
res0: List[List[Symbol]] = List(List('a, 'b, 'c), List('a, 'b, 'd), List('a, 'b, 'e), ...
```


```scala211
def combinations[T](n: Int, x: List[T]): List[List[T]] = {
  
  // obtain the list of all indices
  val index = (0 until x.length).toList    
  def helper(acc: List[List[Int]], m: Int): List[List[Int]] = {
    // accumulates the size of index list
    if (m == 0) acc 
    else helper(for { 
                  lst <- acc; elm <- index; if elm < lst.head 
                } yield elm :: lst, m-1)    
  }
  val init = index map { elm => List(elm) }
  val indexList = helper(init, n-1)
    
  indexList map { ind: List[Int] => ind map { i => x(i) } }
}
val a1 = combinations(1, List('a, 'b, 'c, 'd, 'e, 'f))
a1.length
val a2 = combinations(2, List('a, 'b, 'c, 'd, 'e, 'f))
a2.length
val a3 = combinations(3, List('a, 'b, 'c, 'd, 'e, 'f))
a3.length
val a5 = combinations(5, List('a, 'b, 'c, 'd, 'e, 'f))
a5.length
val a6 = combinations(6, List('a, 'b, 'c, 'd, 'e, 'f))
a6.length
```




    defined [32mfunction[39m [36mcombinations[39m
    [36ma1[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m([33mList[39m([32m'a[39m), [33mList[39m([32m'b[39m), [33mList[39m([32m'c[39m), [33mList[39m([32m'd[39m), [33mList[39m([32m'e[39m), [33mList[39m([32m'f[39m))
    [36mres34_2[39m: [32mInt[39m = [32m6[39m
    [36ma2[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'a[39m, [32m'b[39m),
      [33mList[39m([32m'a[39m, [32m'c[39m),
      [33mList[39m([32m'b[39m, [32m'c[39m),
      [33mList[39m([32m'a[39m, [32m'd[39m),
      [33mList[39m([32m'b[39m, [32m'd[39m),
      [33mList[39m([32m'c[39m, [32m'd[39m),
      [33mList[39m([32m'a[39m, [32m'e[39m),
      [33mList[39m([32m'b[39m, [32m'e[39m),
      [33mList[39m([32m'c[39m, [32m'e[39m),
      [33mList[39m([32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'a[39m, [32m'f[39m),
    [33m...[39m
    [36mres34_4[39m: [32mInt[39m = [32m15[39m
    [36ma3[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'd[39m),
      [33mList[39m([32m'a[39m, [32m'c[39m, [32m'd[39m),
      [33mList[39m([32m'b[39m, [32m'c[39m, [32m'd[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'e[39m),
      [33mList[39m([32m'a[39m, [32m'c[39m, [32m'e[39m),
      [33mList[39m([32m'b[39m, [32m'c[39m, [32m'e[39m),
      [33mList[39m([32m'a[39m, [32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'b[39m, [32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'c[39m, [32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'f[39m),
    [33m...[39m
    [36mres34_6[39m: [32mInt[39m = [32m20[39m
    [36ma5[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'f[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'e[39m, [32m'f[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m),
      [33mList[39m([32m'a[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m),
      [33mList[39m([32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m)
    )
    [36mres34_8[39m: [32mInt[39m = [32m6[39m
    [36ma6[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m([33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m, [32m'd[39m, [32m'e[39m, [32m'f[39m))
    [36mres34_10[39m: [32mInt[39m = [32m1[39m



### P27 (**) Group the elements of a set into disjoint subsets.

a) In how many ways can a group of 9 people work in 3 disjoint subgroups of 2, 3 and 4 persons? Write a function that generates all the possibilities.

Example:

```
scala> group3(List("Aldo", "Beat", "Carla", "David", "Evi", "Flip", "Gary", "Hugo", "Ida"))
res0: List[List[List[String]]] = List(List(List(Aldo, Beat), List(Carla, David, Evi), List(Flip, Gary, Hugo, Ida)), ...
```

b) Generalize the above predicate in a way that we can specify a list of group sizes and the predicate will return a list of groups.

Example:

```
scala> group(List(2, 2, 5), List("Aldo", "Beat", "Carla", "David", "Evi", "Flip", "Gary", "Hugo", "Ida"))
res0: List[List[List[String]]] = List(List(List(Aldo, Beat), List(Carla, David), List(Evi, Flip, Gary, Hugo, Ida)), ...
```

Note that we do not want permutations of the group members; i.e. ((Aldo, Beat), ...) is the same solution as ((Beat, Aldo), ...). However, we make a difference between ((Aldo, Beat), (Carla, David), ...) and ((Carla, David), (Aldo, Beat), ...).

You may find more about this combinatorial problem in a good book on discrete mathematics under the term "multinomial coefficients".


```scala211
def group[T](numbers: List[Int], x: List[T]): List[List[List[T]]] = {
  // return all possible assignments of elements of `x` into groups,
  // where the number of group members are given by `numbers`     
  def allPossibleSplit(x: List[T], m: Int): List[(List[T], List[T])] = {
    // returns all possible ways of spliting `x` 
    // into two groups of sizes m and x.length - m
    val x1: List[List[T]] = combinations(m, x)
    val x2: List[List[T]] = x1 map { lst => (x.toSet diff lst.toSet).toList }
    x1.zip(x2) 
  }
    
  def helper(acc: List[(List[List[T]], List[T])], nums: List[Int]): List[List[List[T]]] = {
    nums match {
      case Nil => acc.map(_._1)  
      case n :: xs => {
        val accNew: List[(List[List[T]], List[T])] = acc
          .map { pair => allPossibleSplit(pair._2, n).map(y => (y._1 :: pair._1, y._2)) }
          .foldLeft(Nil: List[(List[List[T]], List[T])]) { (a, b) => a ::: b }
        helper(accNew, xs)  
      } 
    } 
  }
  
  helper(List((Nil, x.reverse)), numbers.reverse)  
}


def group3[T](x: List[T]): List[List[List[T]]] = {
  group(List(2, 3, 4), x)  
}


val ans1 = group3(List("Aldo", "Beat", "Carla", "David", "Evi", "Flip", "Gary", "Hugo", "Ida"))
ans1.length

val ans2 = group(List(2, 2, 5), List("Aldo", "Beat", "Carla", "David", "Evi", "Flip", "Gary", "Hugo", "Ida"))
ans2.length

// number of ways splitting n objects into (n_1, n_2, ..., n_k) = n! / (n_1! n_2! ... n_k!)
// for n = 9, and (2, 3, 4):
def factorial(n: Int): Int = { if (n <= 1) 1 else n*factorial(n-1) }
factorial(9) / (factorial(2) * factorial(3) * factorial(4))
// for n = 9 and (2, 2, 5):
factorial(9) / (factorial(2) * factorial(2) * factorial(5))
```




    defined [32mfunction[39m [36mgroup[39m
    defined [32mfunction[39m [36mgroup3[39m
    [36mans1[39m: [32mList[39m[[32mList[39m[[32mList[39m[[32mString[39m]]] = [33mList[39m(
      [33mList[39m(
        [33mList[39m([32m"Aldo"[39m, [32m"Beat"[39m),
        [33mList[39m([32m"Evi"[39m, [32m"Carla"[39m, [32m"David"[39m),
        [33mList[39m([32m"Ida"[39m, [32m"Hugo"[39m, [32m"Gary"[39m, [32m"Flip"[39m)
      ),
      [33mList[39m(
        [33mList[39m([32m"David"[39m, [32m"Beat"[39m),
        [33mList[39m([32m"Evi"[39m, [32m"Carla"[39m, [32m"Aldo"[39m),
        [33mList[39m([32m"Ida"[39m, [32m"Hugo"[39m, [32m"Gary"[39m, [32m"Flip"[39m)
      ),
      [33mList[39m(
    [33m...[39m
    [36mres82_3[39m: [32mInt[39m = [32m1260[39m
    [36mans2[39m: [32mList[39m[[32mList[39m[[32mList[39m[[32mString[39m]]] = [33mList[39m(
      [33mList[39m(
        [33mList[39m([32m"Aldo"[39m, [32m"Beat"[39m),
        [33mList[39m([32m"Carla"[39m, [32m"David"[39m),
        [33mList[39m([32m"Ida"[39m, [32m"Hugo"[39m, [32m"Gary"[39m, [32m"Flip"[39m, [32m"Evi"[39m)
      ),
      [33mList[39m(
        [33mList[39m([32m"David"[39m, [32m"Beat"[39m),
        [33mList[39m([32m"Carla"[39m, [32m"Aldo"[39m),
        [33mList[39m([32m"Ida"[39m, [32m"Hugo"[39m, [32m"Gary"[39m, [32m"Flip"[39m, [32m"Evi"[39m)
      ),
      [33mList[39m(
    [33m...[39m
    [36mres82_5[39m: [32mInt[39m = [32m756[39m
    defined [32mfunction[39m [36mfactorial[39m
    [36mres82_7[39m: [32mInt[39m = [32m1260[39m
    [36mres82_8[39m: [32mInt[39m = [32m756[39m



### P28 (**) Sorting a list of lists according to length of sublists.
    
a) We suppose that a list contains elements that are lists themselves. The objective is to sort the elements of the list according to their length. E.g. short lists first, longer lists later, or vice versa.

Example:

```scala    
scala> lsort(List(List('a, 'b, 'c), List('d, 'e), List('f, 'g, 'h), List('d, 'e), List('i, 'j, 'k, 'l), List('m, 'n), List('o)))
res0: List[List[Symbol]] = List(List('o), List('d, 'e), List('d, 'e), List('m, 'n), List('a, 'b, 'c), List('f, 'g, 'h), List('i, 'j, 'k, 'l))
```

b) Again, we suppose that a list contains elements that are lists themselves. But this time the objective is to sort the elements according to their length frequency; i.e. in the default, sorting is done ascendingly, lists with rare lengths are placed, others with a more frequent length come later.

Example:

```scala
scala> lsortFreq(List(List('a, 'b, 'c), List('d, 'e), List('f, 'g, 'h), List('d, 'e), List('i, 'j, 'k, 'l), List('m, 'n), List('o)))
res1: List[List[Symbol]] = List(List('i, 'j, 'k, 'l), List('o), List('a, 'b, 'c), List('f, 'g, 'h), List('d, 'e), List('d, 'e), List('m, 'n))
```

Note that in the above example, the first two lists in the result have length 4 and 1 and both lengths appear just once. The third and fourth lists have length 3 and there are two list of this length. Finally, the last three lists have length 2. This is the most frequent length.


```scala211
def lsort[T](x: List[List[T]]): List[List[T]] = {
  x.sortWith((u: List[T], v: List[T]) => u.length < v.length)  
} 
lsort(List(List('a, 'b, 'c), List('d, 'e), List('f, 'g, 'h), 
           List('d, 'e), List('i, 'j, 'k, 'l), List('m, 'n), List('o)))

def lsortFreq[T](x: List[List[T]]): List[List[T]] = {
  val freqMap: Map[Int, Int] = x.groupBy(_.length).mapValues(_.length)
  x.sortWith((u: List[T], v: List[T]) => freqMap(u.length) < freqMap(v.length))
}
lsortFreq(List(List('a, 'b, 'c), List('d, 'e), List('f, 'g, 'h), 
               List('d, 'e), List('i, 'j, 'k, 'l), List('m, 'n), List('o)))
```




    defined [32mfunction[39m [36mlsort[39m
    [36mres96_1[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'o[39m),
      [33mList[39m([32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'm[39m, [32m'n[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m),
      [33mList[39m([32m'f[39m, [32m'g[39m, [32m'h[39m),
      [33mList[39m([32m'i[39m, [32m'j[39m, [32m'k[39m, [32m'l[39m)
    )
    defined [32mfunction[39m [36mlsortFreq[39m
    [36mres96_3[39m: [32mList[39m[[32mList[39m[[32mSymbol[39m]] = [33mList[39m(
      [33mList[39m([32m'i[39m, [32m'j[39m, [32m'k[39m, [32m'l[39m),
      [33mList[39m([32m'o[39m),
      [33mList[39m([32m'a[39m, [32m'b[39m, [32m'c[39m),
      [33mList[39m([32m'f[39m, [32m'g[39m, [32m'h[39m),
      [33mList[39m([32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'd[39m, [32m'e[39m),
      [33mList[39m([32m'm[39m, [32m'n[39m)
    )



### P31 (**) Determine whether a given integer number is prime.

```scala
scala> 7.isPrime
res0: Boolean = true
```


```scala211
import sys.process._

val cmd = Seq("jupyter", "nbconvert", "--to=html", "S-99 Ninety-Nine Scala Problems.ipynb")
cmd.!!

val cmd2 = Seq("jupyter", "nbconvert", "--to=markdown", "S-99 Ninety-Nine Scala Problems.ipynb")
cmd2.!!
```

    [NbConvertApp] Converting notebook S-99 Ninety-Nine Scala Problems.ipynb to html
    [NbConvertApp] Writing 457066 bytes to S-99 Ninety-Nine Scala Problems.html
    [NbConvertApp] Converting notebook S-99 Ninety-Nine Scala Problems.ipynb to markdown
    [NbConvertApp] Writing 34929 bytes to S-99 Ninety-Nine Scala Problems.md





    [32mimport [39m[36msys.process._
    
    [39m
    [36mcmd[39m: [32mSeq[39m[[32mString[39m] = [33mList[39m(
      [32m"jupyter"[39m,
      [32m"nbconvert"[39m,
      [32m"--to=html"[39m,
      [32m"S-99 Ninety-Nine Scala Problems.ipynb"[39m
    )
    [36mres14_2[39m: [32mString[39m = [32m""[39m
    [36mcmd2[39m: [32mSeq[39m[[32mString[39m] = [33mList[39m(
      [32m"jupyter"[39m,
      [32m"nbconvert"[39m,
      [32m"--to=markdown"[39m,
      [32m"S-99 Ninety-Nine Scala Problems.ipynb"[39m
    )
    [36mres14_4[39m: [32mString[39m = [32m""[39m


