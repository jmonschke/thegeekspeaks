---
date: "2015-03-27T02:23:27Z"
tags:
- web-development
- php
title: 2 Ways To Find Current Directory in PHP Without Regular Expressions
---

There comes a time when you need to find the current directory in PHP, test to see if it is the directory that you expect it is, and take an action based on the test results. Obviously, the easiest way to get the current working directory in PHP is `getcwd()`. However, parsing the output of this function can provide some interesting challenges.

While it is trivial to do this sort of search with a Regular Expression, I tend to look for a solution that is easier to understand its functionality without reaching for the reference books. As a result, I would typically use one of the two methods below. One thing to note is that in each scenarion, any directory name in the path will match, not just the current directory. This can be easily updated to only match the single current directory the script is executed from.

* **Tokenize the path** -- This involves splitting the result of `getcwd()` based on the directory separator, and in *nix operating systems, that is the forward slash `/`. It works out to something like is shown below. One note about this method is that it only works when you have a complete match between the `$desired_path` and the actual directory name. You can easily change this to have the `$desired_path` do a partial match against the `$token`.

```
function find_folder_token() {	
    $path = getcwd();
	$tokens = explode('/', $path);
	$desired_path = 'some_folder';

	foreach ($tokens as $token) {
		if ($token == $desired_path) {
    		return true;
    	}
	}
	return false;
}
```

* **String Search** -- This is a much simpler method to finding whether you are in the desired directory or not, but it does provide its challenges. One such challenge is that by default, it allows you to find partial directory names, which may or may not be what you desire. The way it is displayed below only finds complete directory names. Please note the added forward slashes, `/`, in the `$path` variable as well as the `$desired_path` variable. These are required to make sure to match the full directory name.  

```
function find_folder_search() {
	$path = getcwd() . '/';
    $desired_path = '/some_folder/';
    
    if (strpos($path, $desired_path) !== false) {
    	return true;
    }
    return false;
}
```