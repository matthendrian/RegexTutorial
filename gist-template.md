# Regex in Email Matching

Breaking down Regex in Email Matching. 


## Regex Summary
Regular Expressions, or "Regex", are a critical validation component for when users are passing information from the frontend to a data structure. But why is this true? How does it work, and when is it useful?  I will be giving a high level overview of what Email Regex does, why it is useful, and break it down into each of its base components so you can deploy Regex in your own application. 



## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

At it's core, a regular expression is simply a sequence of characters that defines a search pattern. The components of this search pattern include anchors, quantifiers, grouping constructs, bracket expressions, character classes, the OR operator flags, and character escapes. All together, these components can be daunting, but are much more digestable when broken down. 

Today we will be covering the email regex, this would look something like: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`. Let's break this down. 


### Anchors
Anchoring is helpful when searching for an expression that begins or ends with a string. This utilizes the characters of "$" and "^", denoting the use of a string for the entire expression or for a subexpression within the Regex respectively. Anchoring is useful when dealing with search queries that you know will be in string, such as email addresses and usernames. However, anchoring is less useful when searching for things that are stricly numbers, such as social security numbers or phone numbers. 

### Quantifiers
Quantifiers work inside of bracket expressions, and define the specific length of match that a search query is looking for in terms of characters. This can be strict, or it can fall within a range. If a query length is supposed to only contain 4 characters, like when searching for the last four digits of a phone number, the quantifier would look like {4}. However, if you wanted to search for a phone number using a minimum of 3 digits, and a maximum of 10, your quantifier would look like {3,10}. In the context of an email, quantifiers are helpful when expecting certain numbers of characters, like searching specific domains. 

### Grouping Constructs
Just as how PEMDAS is critical to solving mathematical equations using order of operations, grouping constructs are crucial to creating prescedence in regular expressions. Accomplishing this task can be completed by utilziing parenthesis. Grouping constructs are integral to email matching, since an email is essentially broken down into two distinct parts: before the '@' symbol, and after it. 

This portion of the email is likely to contain an extremly wide variety of letters, characters, and numbers, as well as having no hard character limit. Therefore, this section needs its grouping constructs to be flexible to account for this wide range of possible inputs to include all possible inputs. This would look something like ([a-z0-9_\.-]+). 

The second half of the email validation is more confined, since there is a lesser probability of a domain including special characters, and enforce a stricter character limit. Therefore, the second grouping that handles the domain would look something like ([a-z\.]{2,6}).

### Bracket Expressions
Bracket expressions denote how many characters your search query is looking over. This is an absolutely crucial component when dealing with known values, such as phone numbers and social security numbers, and for values whose character count varies such as email, it helps optimize the query. For example, in an email bracket expression, we can be pretty sure that our email domain will be at least 2 characters long if its a valid one, so our minimum would be 2. Next, we can be pretty sure that most domains will be less than 6 characters long, so we can set a maximum to six. This allows us to valdiate a domain name that is anywhere between 2 and 6 chars. 

### Character Classes
Character classes are contained within the square brackets of a regular expression, signaling what types of characters to look for. For example, a character class of [a] would return a search of every word with an 'a' in it. When validating emails however, we are going to want more than just one character. To do this, we use a hyphen to denote that characters within an alphabetical range will be used, such as [a-z]. 

In the context of our email validation, the character class of [a-z] lets the search engine know that any email containing letters from a-z will be recognized, and recognized accurately as either a name or a domain. 

### The OR Operator
The "or" operator is one of the most powerful Regex tools there is, because it offers greater flexibility in searching. For example, 
when searching for a phone number, we might was to use the Regex: "/d/d/d" indicating that we are looking for any number between 1-9 over 3
character spaces. However, this would not technically be correct, since phone numbers follow sequencing of 3 digits, 3 digits, 4 digits. Therefore, to make sure our Regex returns the last component of the phone number, we would need to include the OR operator at the end, which would be the forward slash "/". This would allow our search to return a more appropriate response. Now, let's break down our regex for email.

Email Match Regex: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

As we can see, there are two "OR" operators within the matching email regex. The first OR operator essentially signals that any letter,
number, or sybmol can be plugged into the the first half of the email. Following the '@', the final "OR" operator at the end of the expression signals that a domain can contain letters or numbers within a certain character limit. 

In summary, the advantage of the OR operator allows search engines to have greater flexibility, and the email regex is no exception, this lets just one expression be able to handle validating the overwhelming majority of all emails. 

### Flags
Flags are a relatively new introduction to the world of Regex, and certainly have a role to play in email validation depending on what you are searching for. Flags are an optional parameter that allow you to further refine your search given highly specific commands. For example, the flag "i" means to ignore the casing of the expression, while the flag "m" denotes that each line of the search must contain $ or ^, not just the entire expression. 

For our email expression, we could introduct the "i" flag in either grouping construct to signal that casing is unimportant. 

### Character Escapes
Finally, the backslash signifies the boundary of a regular expression. When we see an expression include a backslash, we can be sure that it is the beggining or end. In our email match regex: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, we can see that the entire expression falls between the two backslashes.

## Author
Matt Hendrian is a Communications Specialist studying full stack development, covering topics in tech.

(profile link)
