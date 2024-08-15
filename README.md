# Regex
# REGULAR EXPRESSIONS - To find patterns in strings.
A regular expression is a cryptic looking string that describes a search pattern.

^S.+a
S[a-t]*$
\w{9}

1. here ^ and $ sign describes a position.
2.  \w and [a-t] both describes a set of characters.
3. + and * and {9} all describes quantifiers. - the way to specify the number of character occurences.


^ this symbol is used to match a start of a string.
$ this symbol is used to match all the strings which ends with a certain letter.(for example: $a will find all the strings which ends with ‘a’).
\d is used to match a numberical digit. This regex will scan each strings and look for a single numberical digit.
\s to match a white space.
\w to match any name, any digit or underscore, to match any letters in lower or upper case. = \w matches a-z, A-Z, 0-9, _


Q. ^\w\w\w\w\s  - this regex will only follow the 4 letters in first name.

# QUANTIFIERS

This is an way to specify the number of copies of an expressions.

•         0+
?         0 or 1
+        1+ (positive number of occurrences)
{n}     Exactly n occurrences


Examples:
[aeiou]{2}  ------ This will search exactly 2 vowels in a row.
^\w{7}$ ------- This will search exactly 7 letters of characters, not more not less. The $ sign is requires at the end for this REGEX to maintain the decorum.
\w{7} ------ This will search 7 consecutive characters.

# PYTHON RE MODULE EXAMPLES:

import re
-------
------

re.search(pattern,string)   
	#Scans string for first occurence of pattern.
		-  Returns a match object that evaluates to True. (^\w+ \w+$ --- This will only print the firstname and the lastname from the list and will exclude all the single names or names with 3 words. Even an extra whilespace will not let this code work.
		- If we add more \s character in this code followed by ^\w+ \S+\w+$ this will take one more white space in the string.
		
Snippet -

		import  re
		 names = ['First name', 
							   ‘First middle last’, 
							   ‘Singlename’]

		regex = ‘C\w*’
		for name in names: #suppost names contains a list of names of different types.
				match = re.search(regex, name)
				if match:
						print(name) #it will print the name. if there's a match then it will display the details.
						print(match.start()) -- Start and the End value are the indicies which will show you where the match occured.
						print(match.end()
						print(match.span()) -- To call both the indicies in a single call with span method
						print(match.group()) -- To display the substring that matched the REGEX - call the group() method.
						
			to print each matching group of characters by index - 
			
			we will use ( and ) symbol to group the REGEX. for ex: ‘^(\w+)\s+(\w+)$’
						print(name)
						print(match.group(1))
						print(match.group(2))      #It will print the full name first, then will print the firstname and the lastname separately.
						
						#TO give name for this REGEX's each group ‘^(\w+)\s+(\w+)$’ - We can use ?p<groupname> ------- ‘^(?P<group1>\w+)\s+(?P<group2>\w+)$’
						#To print each group by name --
						


we can create our custom character set -

To do this, list the characters in character sets inside square backets.

regex = ‘^[a-zA-z!]+$’ -→ This expression will match any string that is a positive number of lowercase letters. uppercase letters, or an exclamation mark.


Other Search funtions in RE module in python.
→  Often time a REGEX will match a several parts of a string. → The search function just returns the first match. To find them all we will use findall function.

ex:
		re.findall(pattern, string, flags=0)
		--> Retrun all non-overlapping matches of pattern in string, as a list of strings or tuples.
		
		# Scan for blocks of lower case letters
		regex = ‘[a-z]+’
		for name in names:
			matches = re.findall(regex, name)
			if matches:
					print(matches) → This function will return a list of strings, not match objects.
					
			If you would prefer to have access to each match object, call the “find iter” function and loop over the iterator.
			ex:
			re.finditer(pattern, string, flags=0)
			
			match function = this will test a REGEX to test a string for a match from the beginning. 
			Ex:
			
			
			imrpot re
			
			values = ['https://www.google.com',
								 ‘http://www.google.org’,
								 ‘file://file.path.here',
								‘com.android.com.www_https://’]
								
			# TO test which one begins with http and https.
			
			regex = ‘http?' #this will search for the values starting with http.
			for value in values:
				if re.match(regex, value):
					print(value)			
			
			
			O/p - 'https://www.google.com',
								 ‘http://www.google.in’.
								
								
				FULL MATCH FUNCTION -
				
				re.fullmatch(pattern, string, flags=0)       #The fullmatch function is used to not just scan a string for a match, but check to see if the entire string fits the regex.
				
				ex:
				
				regex = ‘https?://w{3}.\w+.(org|com)’
				for value in values:
						if re.fullmatch(regex, value):
								print(value)
								
						O/p - https://www.google.com',
								 ‘http://www.google.org’,.
