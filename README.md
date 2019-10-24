# Autil
Vital, versatile core utility function libray for PHP7 development.


# How to use
- Go to **'@Test/Autil.test.php'** file
- Read and follow instructions in that file.

# Who this is for
I write this functions for my personal use. However, This is also useful for other novice developer.

I think that PHP resources on the web that hit by searching is mostly very old or mostly procedural style. I supposed this is mostly PHP5's feature or earlyer version.  This is useful for deep understanding for intermediate or professional, but for norvice, very boring stuff and complicated.

I'm provably intermediate level.

I write short tutoial in '@Test/autil.test.php' to use this library. written mainly for novice PHP programmers into consideration.

This library make many duplicated, verbose built-in functions bind up to relatively simple functions for daily use.

I convinced that PHP is very norvice-friendly. And as you learn more, and then using many features about OOP or FP, that has been gradually added as time passing, makes learning PHP more interesting!

I curretly has been implementing JavaScript-like OOP features in PHP. This is very interesting. 












# Function Reference
- [Debugging](#debugging)
- [Types](#types)
- [Predicate](#predicate)
- [Each Data Types](#each_data_types)
- - [String](#string)
- - [Array](#array)
- - [Function](#function)

- [HTML](#html)




<h2 id="debugging">Debugging</h2>

#### `_( `*`...any`*` )`
`_ :: * -> * -> ... -> null`
- inject arguments into HTML for debugging

```php
_( [1,2,3] ); // (1, 2, 3)



_( 1, 2, 3 );
// 1 2 3 



_( function(){} );
// [Function]



class Foo{}
_( new Foo() );
// [Object]




$assoc1 = ["name"=> "joe"];
_( $assoc1 );
// [name]: joe



$assoc2 = [
   "type"=> "monk",
   "HP" => "20000",
];
_( $assoc2 );
// [type]: monk
// [HP]: 20000



$assoc3 = [
   "type"=> "monk",
   "HP" => "20000",
   "3" => [
      "2nd" => "hu",
   ],
];
_( $assoc3 );
// [type]: monk
// [HP]: 20000
// [3]:
//   [2nd]: hu



_( "hi", "this", $assoc3 );
// hi this
// [type]: monk
// [HP]: 20000
// [3]:
//   [2nd]: hu
```


#### `pretty( `*`arr`*` )`
`pretty :: ( [] ) -> Null`
- Inject array to HTML that is more easy-to-recognaize format than built-in `print_r()`/`var_dump()`

```php
$flatArr = ["a", "b", "c"];
pretty( $flatArr );
// [0]: a
// [1]: b
// [2]: c


$assocArr = [
   "id" => "001",
   "name" => "buruma",
];
pretty( $assocArr );
// [id]: 001
// [name]: buruma
```



<h2 id="types">Type</h2>

#### `type( `*`any`*` )`
`type :: * -> Str`

- more js-like, easy-to-handle type representation than built-in `gettype()`.

```php
# gettype() (built-in)
gettype( 1 ); // "number"
gettype( "a" ); // "string"
...


# type() 
type( 1 ); // "[Number]"
type( "a" ); // "[String]"
type( [1,2,3] ); // "[Array]"
type( [] ); // "[AssocArray]"
type( function(){} ); // "[Function]"
type( new MyClass() ); // "[Object]"
```


Below table summarize gettype(), type()
|      value     |   type    |  gettype()   |  type()     |
| -------------- | --------- | ------------ | ----------  |
|   `true`, `false`   |  boolean  |  "boolean"   | "[Boolean]" |
|   `null`         |  null     |  "NULL"      | "[Null]"    |
|   `1`, `300`       |  integer  |  "interger"  | "[Number]"  |
|   `2.3`         |  double   |  "double"    |     〃      |
|   `NAN`          |  NAN      |  "double"    |     〃      |
|   `"hi"`        |  string   |  "string"    | "[String]"   |
|   `[1,2]`        |  array    |  "array"     | "[Array]"    |
|   `["name" => "goku"]` | array | "array" | "[AssocArray]" |
|   `new Person()`   |  object   |  "object"    | "[Object"]   |     
|   `function(){}` |  object   |  "object"    | "[Function]" | 





<h2 id="predicate">Predicate</h2>

#### `isType( `*`any`*`, `*`typeStr`*` )`
`isType :: * -> Str -> Bool`
- Return true if first argument type match specified type by typeStr

```php
isType( "a", "[String]" ); // true
isType( 1, "[Number]" ); // ture
```



#### `isTypeLiteral( `*`str`*` )`
`isTypeLiteral :: Str -> Str`
- Return true if input string is "[Number]" \| "[String]" \| "[Boolean]" \|...

```php
isTypeLiteral("a"); // false
isTypeLiteral("[Function]" ); // true
isTypeLiteral("[function]" ) ; // false
```







<h2 id="each_data_types">Each Data Type</h2>
<h3 id="string">String</h3>

#### `length( `*`str`*` )`
`length :: * -> Num`
- Return length of String. Equivalent to built-in `strlen()`.

\*`length()` function also accept different data types, Array, Function, Object. About more detail, see corresponding section of `length()`.


```php
length( "a" ); // 1
length( "abcd" ); // 4
```


#### `prepend( `*`str`*` )`
`prepend :: Str -> Num`
- Return 

```php

```


#### `appned( `*`str`*` )`
`appned :: Str -> Num`
- Return 

```php

```


#### `split( `*`separator`*`, `*`str`*` )`
`split :: Str -> []`
- Return the array that element is divided string accoding to separator. This function can acccept `""`(empty string) as *`separator`*.

```php
$str = "this is demo";
_( split("", $str) ); // (t, h, i, s, , i, s, , d, e, m, o)

// `split()` can accept empty string as `separatir`. (it is illegal in built-in `explode()` function of which the separator is empty string. If you want to do like those, instead you need to use `str_split()` function.)
// `split()` is the merged version of `str_split()` and `explode()`.


_( split(" ",$str) ); // (this, is, demo)
```



#### `toUpperCase( `*`str`*` )`
`toUpper :: Str -> Str`
- Return all upper-cased string.

```php
$str = "lower-case letter";

_( toUpperCase($str) );  // LOWER-CASE LETTER
```


#### `toLowerCase( `*`str`*` )`
`toUpper :: Str -> Str`
- Return all lower-cased string.

```php
$str = "UPPER-CASE LETTER";

_( toLowerCase($str) );  // lower-case letter";
```


#### `toCapitalCase( `*`str`*` )`
`toCapitalCase: Str -> Str`
- Return capitalized string.

```php
$str = "lower-case letter";

_( toCapitalCase($str) );  // Lower-case letter
```











<h3 id="array">Array</h3>

#### `length( `*`arr`*` )`
`length :: * -> Num`
- Return length of the array. Equivalent to built-in `sizeof()`, `count()`.

```php
length( [1,2,3] ); // 3
```


#### `isAssoc( `*`any`*` )`
`isAssoc :: * -> Bool`
- Return true if passed argument is Associative array.

```php
$flatArr = [1,2,3];
$assocArr = [
   "id" => "001",
   "name" => "goku"
];

isAssoc( $flatArr ); // false
isAssoc( $assocArr ); // true
```


#### `head( `*`arr`*` )`
head :: [] -> *
- Return first element of `arr`

```php
$arr = ["a", "b", "c"];

head( $arr ); // "a"
```



#### `last( `*`arr`*` )`
last :: [] -> *
- Return last element of array `arr`

```php
$arr = ["a", "b", "c"];

last( $arr ); // "c"
```



#### `rest( `*`arr`*` )`
rest :: [] -> []
- Return copied `arr` array except first elements

```php
$arr = ["a", "b", "c"];

rest( $arr ); // ("b", "c")
```

#### `initial( `*`arr`*` )`
rest :: [] -> []
- Return copied `arr` array except last elements

```php
$arr = ["a", "b", "c"];

rest( $arr ); // ("a", "b")
```


#### `push( `*`val`*`, `*`arr`*` )`
push :: (* -> []) -> []
- insert `val` to end of array `arr`. return item-inserted new array. Original `arr` is not affected.

```php
$arr = [1, 2, 3];

_( push(4, $arr) ); // (1, 2, 3, 4)
_( $arr ); // (1, 2, 3)
```


# pop
# shit 
# unshift




#### `pushTo( `*`val`*`, `*`index`*`, `*`arr`*` )`
pushTo :: (* -> Number -> []) -> *
- push `val` into specified position `index` on `arr`. pre-existed element and rest of element are pushed back. Return new merged array. Original array is not affected.

```php
$arr = [1,2,3,4];
$pushedArr = pushTo("+", 2, $arr);

_( $pushedArr ); // (1, 2, +, 3, 4)
_( $arr ); // (1, 2, 3, 4)
```



#### `take( `*`num`*`, `*`arr`*`)`
take :: (Number -> []) -> []
- take specified number `num` of elements from start in array and return new taked array.

```php
$arr = [1,2,3,4];
 
take(1, $arr); // (1)
take(2, $arr); // (1, 2)
take(3, $arr); // (1, 2, 3)
```



#### `takeAt( `*`startIndex`*`, `*`num`*`, `*`arr`*`)`
takeAt :: (Number -> Number -> []) -> []
- take specified number `num` of elements from `startIndex` in array and return new taked array.

```php
$arr = [1,2,3,4];

takeAt(1, 2, $arr); // (2, 3)
takeAt(2, 2, $arr); // (3, 4)
takeAt(1, 3, $arr); // (2, 3, 4)
```



#### `concat( `*`val1`*`, val2 )`
`concat :: (...*) -> []`
- If all arguments are string, return concatenated string.
- If all arguments are **not** string, return concatenated array.

```php
concat("abc", "foo"); // "abcfoo"
concat("abc", "foo", "Hey"); // "abcfooHey"


concat(1, 2); // (1, 2)
concat(1, 2, 3); // (1, 2, 3)


concat([1], [2]); // (1, 2)
concat([3], ["a", "b"]); // (3, "a", "b")
```



#### `indexOf( `*`ArrItem`*`, `*`arr`*` )`
`indexOf :: (* -> []) -> Num`
- Return index of element in array/assocArray. If isn't, return `false`.

```php
$flatArr = ["a", "b", "c"];

indexOf("c", $flatArr); // 2


$assocArr = [
   "id" => "001",
   "name" => "goku",
];

indexOf("name", $AssocArr); // 1
```


##### `joinWith( `*`jointer`*`, `*`...strs`*` )`
`joinWith :: (String -> ...String) -> String`
- join list of string arguments with `jointer`

```php
joinWith("=", "a", "b" ); // a=b
joinWith("", "a", "b"); // ab
joinWith("=", "a", "b", "c" ); // a=b=c
joinWith("", "a", "b", "c"); // abc
```



#### `_forEach( `*`fn`*`, `*`arr`*` )`
`_forEach :: (fn -> []) -> null`
- applying function `fn` to each element in array `arr`. no return value.

parameter
   arr:
      normal(flat) array or associative array
   
   callback( $key, $val, $index, $arr):
      function that is invoked on each item.
   
      callback function on each item in array.
      (1) when passed array is normal arr
         $key: null
         $val: current iteration value in array
         $index: current iteration index
         $arr: target array
         
      (2) when passed array is assoc arr
         $key: current iteration key in ssocArray
         $val: current iteration value in ssocArray
         $index:current iteration index in ssocArray
         $arr: target array
   
```php
#####  flatArr  #####
$flatArr = ["a", "b", "c"];

_forEach( function($key, $val, $indx, $arr){
   _( "key: {$key}, val: {$val}, index: {$indx}" );
}, $flatArr );

//----- output -------------
// key: , val: a, index: 0
// key: , val: b, index: 1
// key: , val: c, index: 2

/*--- function can be passed by variable name --------
$injectKeyVals = function($key, $val, $indx, $arr){
   _( "key: {$key}, val: {$val}, index: {$indx}" );
};
_forEach( $injectKeyVals, $flatArr );
/*--------------------------------------------------*/



#####  assocArr  #####
$assocArr = [
   "id" => "001",
   "name" => "bejita",
];

_forEach( function($key, $val, $indx, $arr){
   _( "key: {$key}, val: {$val}, index: {$indx}" );
}, $assocArr );

//----- output -------------------
// key: id, val: 001, index: 0
// key: name, val: bejita, index: 1
/*------------------------------*/
```



#### `map( `*`mappingFn`*`, `*`arr`*` )`
`map :: ((* -> *) -> []) -> []`
- applying function `mappingFn` to each element of array `arr` and return new mapped array.

```php
$arr = [1,2,3];
$add1 = function($x){
   return $x + 1;
};

_( map($add1, $arr) ); // (2,3,4)
```



#### `filter( `*`predicateFn`*`, `*`arr`*` )`
`filter` :: ((* -> bool) -> []) -> []
- filtering elements of array with `predicateFn` and return new filtered array.

```php
#-----  arr  ----------------------
$arr = [1, 2, 3, 4];
$isEven = function($x){
   return $x % 2 === 0;
};

_( filter($isEven, $arr) ); // 2, 4



#-----  assocArr  -----------------
$assocArr = [
   "one" => 1,
   "two" => 2,
];
$isEven_assoc = function($key, $val){
   return $val % 2 === 0;
};

_( filter($isEven_assoc, $assocArr) );
//--- output ----------
// [0]:
//   [two]: 2   /**/
```



#### `reduce( `*`reducerFn`*`, `*`initVal`*`, `*`arr`*` )`
`reduce :: ((* -> * -> *) -> * -> []) -> *`

```php

```



#### `some( `*`predicateFn`*`, `*`arr`*` )`
`some :: ((* -> bool) -> []) -> bool`
- Return true if at least one element satisfy condition of `predicateFn`.

```php
$arr = [1,2,3];

some(function($curr){
   return $curr === 3;
}, $arr); // true

some(function($curr){
   return $curr < 2;
}, $arr); // true



// function can be passed by variable name
$isThree = function($curr){
   return $curr === 3;
};
some( $isThree, $arr ); // true


$lessThan2 = function($curr){
   return $curr < 2;
};
some( $lessThan2, $arr) ); // true
```


#### `every( `*`predicateFn`*`, `*`arr`*` )`
`every :: ((* -> bool) -> []) -> bool`
- Return true if all element satisfy condition of `predicateFn`.

```php
$arr = [1,2,3];

every(function($curr){
    return $curr <= 3;
}, $arr); // true

every(function($curr){
    return $curr <= 2;
}, $arr); // false


// function can be passed by variable name
$lessThanEq3 = function($curr){
    return $curr <= 3;
};

every($lessThanEq3, $arr); // true



$lessThanEq2 = function($curr){
    return $curr <= 2;
};

every($lessThanEq2, $arr); // false
```



#### `prettify( `*`arr`*` )`
`prettify :: [] -> Str`
- Return string that is more human-readable format than built-in `print_r()`/`var_dump()`.

```php
$flatArr = [1, 2, 3];
exho( prettify($flatArr) ); // (1, 2, 3)



$assocArr = [
   "name" => "goku",
];
exho( prettify($assocArr) );
// [name]: goku




$assocArr2d = [
   "name" => "goku",
   "mode" => [
      "kaiouken" => "speedx50",
      "superSiya" => "MUTEKI!",
   ],
];
exho( prettify($assocArr2d) );
// [name]: goku
// [mode]:
//   [kaiouken]: speedx50
//   [superSiya]: MUTEKI!
```











<h3 id="function">Function</h3>

#### `length( `*`any`*` )`
`length :: * -> Num`
- Return paremter length of the function.

```php
$add = function ($x, $y){
   return $x + $y;
};
length( add ); // 2
```


#### `call( `*`fn`*`, `*`...args`*` )`
`call :: (fn -> ...*) -> *`
- call `fn` with arbitrary-length list of arguments.

```php

```


#### `apply( `*`fn`*`, `*`arrArg`*` )`
`apply :: (fn -> []) -> *`
- call `fn` with arguments of array `addArg`.

```php

```

#### bind

#### curry

#### toClosure











<h2 id="html">HTML</h3>

#### pretty



#### `inject( `*`str`*`, `*`tagName="h1"`*`, `*`attrs=[]`*` )`
`inject :: (Str -> Str -> []) -> null`
- Inject string to HTML. embracing tagName(for HTML tgaName), attrs(for HTML attributes)

```php
inject( "hi" );
//*** output(HTML source code) ***
// <h1>hi</h1>

inject( "hey!", "h2" );
// <h2>hey!</h2>

$attrArray = [
   "class" => "item",
   "style" => "color: red;",
];
inject( "hoi.", "h3", $attrArray );
// <h3 class="item" style="color: red;">hoi.</h3>

```


#### `toAttr( `*`assocArr`*` )`
`toAttr :: [] -> Str`
- convert associative array to string for HTML attribute format( 'Attribute="value"' )

```php

```
