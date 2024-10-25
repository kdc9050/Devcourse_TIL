## 연습문제 + 풀이

```js
//1 특정 문자 제거
function removeChar(str, char) {
  let result = "";
  for (let i = 0; i < str.length; i++) {
    if (str[i] !== char) {
      result += str[i];
    }
  }
  return result;
}
console.log(removeChar("hello world", "o")); // "hell wrld"

// 1- 강사님 풀이 - replaceAll 사용 하면 되긴함
function removeChar(str, char) {
  let result = "";
  for (let i = 0; i < str.length; i++) {
    if (str[i] !== char) result += str[i];
  }
  return result;
}
console.log(removeChar("hello world", "o")); // "hell wrld"
```

```js
//2 배열 요소를 반전
function reverseArray(arr) {
  let results = [];

  for (let i = arr.length - 1; i >= 0; i--) {
    results.push(arr[i]);
  }
  return results;
}
console.log(reverseArray([1, 2, 3, 4, 5])); // [5, 4, 3, 2, 1]

/// 2- 강사님 풀이 - reverse 사용하면 되긴함
// 반전 -> 뒤집다
function reverseArray(numArr) {
  const reversed = [];
  for (let i = numArr.length - 1; i >= 0; i--) {
    reversed.push(numArr[i]);
  }
  return reversed;
}
console.log(reverseArray([1, 2, 3, 4, 5])); // [5, 4, 3, 2, 1]
```

```js
//3 특정 숫자 찾기
function containsNumber(arr, n) {
  let isPrime = false;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === n) {
      isPrime = true;
      break;
    }
  }
  return isPrime;
}
console.log(containsNumber([1, 2, 3, 4, 5], 5)); //true
console.log(containsNumber([1, 2, 3, 4, 5], 7)); //flase

///// 3- 강사님 풀이 - includes 사용하면 되긴함
//
function containsNumber(numArr, num) {
  for (let n of numArr) {
    if (n === num) return true;
  }
  return false;
}
console.log(containsNumber([1, 2, 3, 4, 5], 51)); // true
// containsNumber([1, 2, 3, 4, 5], 7); // false
```

```js
//4 애너그램인지 확인 - 1,2 알파벳의 갯수가 똑같은지만 확인 하면 됨
function isAnagrams(word1, word2) {
  let result = true;
  let word1Count = [];
  let word2Count = [];
  for (let i = 0; i < word1.length; i++) {
    if (word1Count[word1[i]]) {
      word1Count[word1[i]]++;
    } else {
      word1Count[word1[i]] = 1;
    }
  }
  for (let i = 0; i < word2.length; i++) {
    if (word2Count[word2[i]]) {
      word2Count[word2[i]]++;
    } else {
      word2Count[word2[i]] = 1;
    }
  }
  for (let key in word1Count) {
    if (word1Count[key] !== word2Count[key]) {
      result = false;
      break;
    }
  }
  return result;
}

console.log(isAnagrams("listen", "silent")); //true
console.log(isAnagrams("fluster", "restful")); //true
console.log(isAnagrams("rat", "car")); //false
console.log(isAnagrams("aaa", "aaaa")); //false

// 4- 강사님 풀이
// 애너그램
// 단어를 구성하는 문자의 갯수가 일치하는가 = 애너그램
// 문자의 갯수 -> "aaa" "aaaa"
function isAnagrams(str1, str2) {
  if (str1.length !== str2.length) return false;

  const charCount = {};

  // 0, "", undefeind, null, NaN
  for (let char of str1) {
    charCount[char] = (charCount[char] || 0) + 1;
  }

  for (let char2 of str2) {
    if (!charCount[char2]) return false;
    charCount[char2]--;
  }

  return true;
}
console.log(isAnagrams("lisaen", "silent")); // true
// isAnagrams("fluster", "restful"); // true
// isAnagrams("rat", "car"); // false
// isAnagrams("aaa", "aaaa"); // false
```

```js
//5 배열에서 두 수의 합
function twiceSum(arr, n) {
  let results = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === n) {
        results.push([arr[i], arr[j]]);
      }
    }
  }
  return results;
}
console.log(twiceSum([1, 2, 3, 4, 5], 5)); // [[1, 4], [2,3]]
console.log(twiceSum([1, 2, 3, 4, 5], 9)); // [[4, 5]]
console.log(twiceSum([1, 2, 3, 4, 5], 6)); // [[1, 5], [2,4]]

// 5- 강사님 풀이
function twiceSum(numArr, num) {
  const result = [];
  for (let i = 0; i < numArr.length; i++) {
    for (let j = i + 1; j < numArr.length; j++) {
      if (numArr[i] + numArr[j] === num) result.push([numArr[i], numArr[j]]);
    }
  }
  return result;
}
console.log(twiceSum([1, 2, 3, 4, 5], 6)); // [[1, 5], [2,4]]
```

## 연습문제 ++

```js
// 1. 강사님
function compressString(str) {
  let compress = "";
  let count = 0;
  let currentChar = str[0];
  for (let i = 0; i < str.length; i++) {
    if (str[i] === currentChar) count++;
    else {
      compress += currentChar + count;
      currentChar = str[i];
      count = 1;
    }
  }
  compress += `${currentChar}${count}`;
  return compress;
}
console.log(compressString("abbbffd")); //a3b3c3
```

```js
// 2 팰린드롬 확인 하기 (쉬운 버전)
function isPalindrome(str) {
  for (let i = 0; i < str.length / 2; i++) {
    if (str[i] !== str[str.length - 1 - i]) return false;
  }
  return true;
}
console.log(isPalindrome("racecar"));
```

```js
// 3 팰린드롬 확인 하기 (어려운 버전)
function isPalindromeSentence(str) {
  // 문자열에서 순수하게 알파뱃 추출
  // 정규식 -> 정규식 x
  // AI -> 개발 생산선 높아 지는 범위 안에서 적극
  // .replace(/[^a-z]/g, '');
  const cleanedStr = str.toLowerCase().replace(/[^a-z]/g, "");
  const reversed = cleanedStr.split("").reverse().join("");
  return cleanedStr === reversed;
}
console.log(isPalindromeSentence("racecar")); // false
console.log(isPalindromeSentence("A man, a plan, a canal, Panama!")); // true
```

```js
//4. 최대공약수 (GCD)
// 4 알고리즘
// 4. 유클리드 호제법
// 최대 공약수(Greatest Common Divisor, GCD)
// GCD -> 알고리즘 법칩
// 두 수 a b의 최대 공약수는 a 와 b의 나머지가 0이 될 때의 a다
// a, b -> a % b === 0
// a, b의 최대 공약수는 a를 b로 나눴을 때, 나머지가 0일 때의 a 값이다.

// 재귀 함수
// 기저 평가 (base case)
// 재귀 호출

// 10 -> 1, 2, 5, 10
// 2 -> 1, 2

// 18, 24 -> gcd(24, 18)
// 24 18  -> gcd(18, 6)
// 18, 6 -> gcd(6, 0)
// 6, 0 -> 6

// 15, 5 -> gcd(5, 15 % 5)
// 5 , 0 -> 5
function gcd(a, b) {
  if (b === 0) return a;
  return gcd(b, a % b);
}

// console.log(gcd(56, 98)); // 14
// console.log(gcd(101, 10)); // 1
// console.log(gcd(15, 5)); // 5
// console.log(gcd(100, 75)); // 25
// console.log(gcd(18, 24)); // 6

// 최소 공배수(Lower Common Multiple) -> 두 수를 나누어 떨어지게 하는 최대한 작은 수
// 두 수 a , b의 최소 공배수는 ?
// a * b / a, b의 최대 공약수 -> 최소 공배수
// a * b / gcd
function lcm(a, b) {
  return (a * b) / gcd(a, b);
}
console.log(lcm(100, 24)); // 600
```

```js
// 5. 버블정렬
function bubbleSort(numArr) {
  for (let i = 0; i < numArr.length; i++) {
    for (let j = 0; j < numArr.length - 1 - i; j++) {
      // console.log(numArr[j], numArr[j + 1]);
      if (numArr[j] > numArr[j + 1]) {
        // 자리 바꿔줘야함
        // swap 로직
        const temp = numArr[j];
        numArr[j] = numArr[j + 1];
        numArr[j + 1] = temp;
      }
    }
  }
  return numArr;
}
console.log(bubbleSort([5, 4, 8, 10, 2]));
// console.log(bubbleSort([5, 3, 8, 1, 2])); // [1, 2, 3, 5, 8]
```

## 최대공약수 최소 공배수

```js
//1
function solution(n, m) {
  function gcd(a, b) {
    if (b === 0) return a;
    return gcd(b, a % b);
  }
  function lcm(a, b) {
    return (a * b) / gcd(a, b);
  }
  return [gcd(n, m), lcm(n, m)];
}
console.log(solution(3, 12)); // [3, 12]
console.log(solution(2, 5)); // [1, 10]

// 1. 강사님 풀이
// 최대 공약수
function gcd(a, b) {
  if (b === 0) return a;
  return gcd(b, a % b);
}

function solution(a, b) {
  return [gcd(a, b), (a * b) / gcd(a, b)];
}

// 최대 공약수 x 최소 공배수 = a * b
console.log(solution(3, 12)); // [3, 12]
console.log(solution(2, 5)); // [1, 10]
```

```js
//2
function solution(arr) {
  function gcd(a, b) {
    if (b === 0) return a;
    return gcd(b, a % b);
  }
  function lcm(a, b) {
    return (a * b) / gcd(a, b);
  }
  let result = arr[0];
  for (let i = 0; i < arr.length; i++) {
    result = lcm(result, arr[i]);
  }
  return result;
}

console.log(solution([2, 6, 8, 14])); // 168
console.log(solution([1, 2, 3])); // 6
console.log(solution([3, 5, 15])); // 15

//2 강사님 풀이
// 최대 공약수
function gcd(a, b) {
  if (b === 0) return a;
  return gcd(b, a % b);
}

function solution(numArr) {
  let result = numArr[0];
  for (let i = 0; i < numArr.length - 1; i++) {
    result = (result * numArr[i + 1]) / gcd(result, numArr[i + 1]);
  }
  return result;
}

// 최대 공약수 x 최소 공배수 = a * b
console.log(solution([2, 6, 8, 14])); // 168
console.log(solution([1, 2, 3])); // 6
console.log(solution([3, 5, 15])); // 15

// 최대 공약수
function gcd(a, b) {
  if (b === 0) return a;
  return gcd(b, a % b);
}

function solution(numArr) {
  return numArr.reduce((a, b) => (a * b) / gcd(a, b));
}

// 최대 공약수 x 최소 공배수 = a * b
console.log(solution([2, 6, 8, 14])); // 168
console.log(solution([1, 2, 3])); // 6
console.log(solution([3, 5, 15])); // 15
```

## 실행 컨텍스트

/_ 채우기 _/
