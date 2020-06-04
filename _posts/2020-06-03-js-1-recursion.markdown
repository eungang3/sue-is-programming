---
layout: post
title:  "Recursive Algorithm 이해하기"
date:   2020-06-03 17:35:27 +0900
categories: Javascript
---

## Recursive Algorithm이란?
- 어떤 문제를 풀 때, 똑같은 문제를 더 작은 버전으로 만들어서 해결하는 방식.
- fucntion 속에서 스스로를 호출하는 방식으로 활용

<br/>

## Recursive function을 만들기 위해 필요한 3가지
- __A Termination Condition :__ Recursion을 끝내기 위한 조건(잘못된 상황인 경우).  
- __A Base Case :__ Recursion을 끝내기 위한 조건(원하는 값을 얻은 경우)
- __The Recursion :__ function 안에서 스스로를 호출하는 부분.

<br/>
### ex 1) factorial 값 구하기
(출처<sup>1</sup>에서 발췌한 코드)
{% highlight javascript %}
function factorial(x) {
  //Termination
  if (x < 0) return;

  //Base
  if (x === 0) return 1;

  //Recursion
  return x * factorial(x-1);
}

{% endhighlight %}

__factorial(3);으로 호출한 경우:__

factorial(3);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 3 * factorial(2);

factorial(2);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 2 * factorial(1);

factorial(1);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 거짓 -> 계속
3. return 1 * factorial(0);

factorial(0);
1. x가 0보다 작은가? -> 거짓 -> 계속
2. x가 0인가? -> 참 -> return 1;

![recursion1](https://eungang3.github.io/sue-is-programming/assets/recursion1.jpg)

<br/>

### ex 2) string 속 글자 거꾸로 배열하기
(출처<sup>1</sup>에서 발췌한 코드)
{% highlight javascript %}
function revStr(str) {
  //Base, Termination
  if (str === '') return '';

  //Recursion
  return revStr(str.substr(1)) + str[0];
}

{% endhighlight %}

__revStr('dog');으로 호출한 경우:__

revStr('dog');
1. str === ''인가? -> 아님 -> 계속
2. revStr('og') + 'd'

revStr('og');
1. str === ''인가? -> 아님 -> 계속
2. revStr('g') + 'o'

revStr('g');
1. str === ''인가? -> 아님 -> 계속
2. revStr('') + 'g'

revStr('');
1. str === ''인가? -> 참

![recursion2](https://eungang3.github.io/sue-is-programming/assets/recursion2.jpg)

<br/>

### ex 3) Palindrome checker 만들기
(출처<sup>2</sup>에서 발췌한 코드)
{% highlight javascript %}
// Returns the first character of the string str
var firstCharacter = function(str) {
    return str.slice(0, 1);
};

// Returns the last character of a string str
var lastCharacter = function(str) {
    return str.slice(-1);
};

// Returns the string that results from removing the first
//  and last characters from str
var middleCharacters = function(str) {
    return str.slice(1, -1);
};

var isPalindrome = function(str) {
    // Base
    if (str.length === 1 || str.length === 0){
        return true;
    }
   
    // Termination
    if (firstCharacter(str) !== lastCharacter(str)){
        return false;
    }
   
    // Recursion
    return isPalindrome(middleCharacters(str));
};

{% endhighlight %}

__isPalindrome('rotor');로 호출한 경우:__

isPalindrome('rotor');
1. string의 길이가 0이나 1인가? -> 거짓 -> 계속
2. 첫글자와 끝글자가 같은가? -> 참 -> 계속
3. isPalindrome('oto');

isPalindrome('oto');
1. string의 길이가 0이나 1인가? -> 거짓 -> 계속
2. 첫글자와 끝글자가 같은가? -> 참 -> 계속
3. isPalindrome('t');

isPalindrome('t');
1. string의 길이가 0이나 1인가? -> 참 -> return true;

<br/>

### ex 4) 거듭제곱 계산하기
(출처<sup>2</sup>에서 발췌한 코드)
{% highlight javascript %}
function isEven(n) {
    return n % 2 === 0;
};

function isOdd(n) {
    return !isEven(n);
};

function power(x, n) {
   
    // base, termination
    if (n === 0) {
        return 1;
    }
    // recursion(n이 음수인 경우)
    if (n < 0) {
        return 1 / power(x, (-n));  
    }
   
    // recursion(n이 양수이고 홀수인 경우)
    if (isOdd(n)) {
        return power(x, (n-1)) * x;
    }
   
    // recursion (n이 양수이고 짝수인 경우)
    if (isEven(n)) {
        var y = power(x, n/2);
        return y * y;
    }
};

console.log(power(3, 0)); //1 출력
console.log(power(3, 1)); //3 출력
console.log(power(3, 2)); //9 출력
console.log(power(3, -1)); // 3분의 1 출력

{% endhighlight %}

__power(3, 3);으로 호출한 경우 :__

power(3, 3);
1. n이 0인가? -> 거짓 -> 계속
2. n이 음수인가? -> 거짓 -> 계속
3. n이 홀수인가? -> 참 -> return power(3, 2) * 3;

power(3, 2);
1. n이 0인가? -> 거짓 -> 계속
2. n이 음수인가? -> 거짓 -> 계속
3. n이 홀수인가? ->거짓 -> 계속
4. n이 짝수인가? -> 참
- var y = power(3, 1);
- return y * y;

power(3, 1);
1. n이 0인가? -> 거짓 -> 계속
2. n이 음수인가? -> 거짓 -> 계속
3. n이 홀수인가? -> 참 -> return power(3, 0) * 3;

power(3, 0);
1. 1. n이 0인가? -> 참 -> return 1;

<br/>

### ex 5) Array의 N번째까지 곱하기
(출처<sup>3</sup>에서 발췌한 코드)
{% highlight javascript %}
function multiply(arr, n) {
    if (n <= 0) {
      return 1;
    } else {
      return multiply(arr, n - 1) * arr[n - 1];
    }
  }
{% endhighlight %}

__multiply([5, 3, 2, 4], 3)으로 호출한 경우:__
1. n <= 0인가? -> 거짓 -> 계속
2. return multiply([5, 3, 2, 4], 2) * arr[2];

multiply([5, 3, 2, 4], 2)
1. n <= 0인가? -> 거짓 -> 계속
2. return multiply([5, 3, 2, 4], 1) * arr[1];

multiply([5, 3, 2, 4], 0) * arr[0];
1. n <= 0인가? -> 참 -> return 1;

<br/>

### ex 6) n에서 1까지 카운트다운하기
(출처<sup>3</sup>에서 발췌한 코드)
{% highlight javascript %}
function countdown(n){
  //Base case
  if (n < 1) {
    return [];
  } else {
    let countArray = countdown(n - 1);
    countArray.unshift(n)
    return countArray;
  }
}
{% endhighlight %}

__countdown(2);로 호출한 경우 :__

countdown(2);
1. n < 1인가? -> 거짓 -> 계속
2. let countArray = countdown(n - 1);
3. countArray.unshift(2);
4. return countArray; ---> [2, 1]


countdown(1);
1. n < 1인가? -> 거짓 -> 계속
2. let countArray = countdown(n - 1);
3. countArray.unshift(1);
4. return countArray;

countdown(0);
n < 1인가? -> 참 -> return [];

<br/>

### ex 7) 두 숫자 사이의 숫자들로 이루어진 array 만들기
(출처<sup>3</sup>에서 발췌한 코드)
{% highlight javascript %}
function rangeOfNumbers(startNum, endNum) {
  //termination
  if (startNum > endNum) {
    return "invalid input";
  }
  
  //base case
  if (startNum === endNum) {
    return [endNum];
  }

  //recursion
  var numbersArray = rangeOfNumbers(startNum, endNum - 1)
  numbersArray.push(endNum);
  return numbersArray;
};
{% endhighlight %}

__rangeOfNumbers(2, 3);으로 호출한 경우 :__

rangeOfNumbers(2, 3);
1. 2 > 3인가? -> 거짓 -> 계속
2. 2 = 3인가? -> 거짓 -> 계속
3. numbersArray = rangeOfNumbers(2, 2);
4. numbersArray.push(3);
5. return numbersArray --> [2, 3]

rangeOfNumbers(2, 2);
1. 2 > 2인가? -> 거짓 -> 계속
2. 2 = 2인가? -> 참 -> return [2];

<br/><br/>
출처 : <br/>
<sup>1</sup> Morelli, B. (2017, August 21). Learn and Understand Recursion in JavaScript. Retrieved June 03, 2020, from [https://codeburst.io/learn-and-understand-recursion-in-javascript-b588218e87ea](https://codeburst.io/learn-and-understand-recursion-in-javascript-b588218e87ea),<br/>
<sup>2</sup>재귀란? (개념 이해하기) | 재귀 알고리즘 | 칸아카데미. (n.d.). Retrieved June 03, 2020, from [https://ko.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion](https://ko.khanacademy.org/computing/computer-science/algorithms/recursive-algorithms/a/recursion),<br/>
<sup>3</sup> FreeCodeCamp.org. (n.d.). Retrieved June 04, 2020, from [https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/replace-loops-using-recursion](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/basic-javascript/replace-loops-using-recursion)