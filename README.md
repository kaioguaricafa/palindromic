var test_values = [2, 3];

function run_function(func, test_values) {
  for(var i in test_values){
    console.log('Test value:', test_values[i]);
    var t0 = performance.now();
    console.log('Output:', func(test_values[i]));
    var t1 = performance.now();
    console.log("Took " + (t1 - t0) + " ms");
    console.log();
  }
}

function is_palindrome(initial_number) {
  var reversed = 0;
  var temp = initial_number;
  while (temp > 0) {
    var last_digit = temp % 10; // extract the last digit
    reversed = reversed * 10 + last_digit; // add last digit
    temp = parseInt(temp / 10); // remove last digit
  }
  return initial_number === reversed;
}


function largestPalindromeProduct(n) {
  return brute_force(n)
}

function brute_force(n){
  var largest_number = Math.pow(10, n) -1;
  var smallest_number = Math.pow(10, (n-1));
  var largest_palindrome = 0;

  for(var outer_i=largest_number; outer_i>smallest_number; outer_i--){
    for(var inner_i=outer_i; inner_i>smallest_number; inner_i--){
      var number = outer_i * inner_i;
      if(is_palindrome(number) && number>largest_palindrome){
        largest_palindrome = number;
        if(inner_i>smallest_number){
          smallest_number = inner_i;
        }
        break;
      }
    }
  }
  return largest_palindrome;
}

run_function(largestPalindromeProduct, test_values);
