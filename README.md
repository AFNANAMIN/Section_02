# Section_02
Bulls &amp; Cows Word Console Game

### Coding Standards

- [Unreal Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard/index.html)
- [Live Google Slides](https://docs.google.com/presentation/d/1gEO7kcJPvWjGySQjxD7z0OcGNpFUNccEvR9cCJG04D0/edit#slide=id.gf8b855009_5_1)
- [Developer's discussion](https://community.gamedev.tv/tags/c/unreal/s02-bullcows/urc_s02_bull_cow_game_overview)


## Bulls and Cows


### Using, #include and Namespaces

- hash include
- preprocessor directive
- cut and paste contents of file to the header of the cpp file at the time you say build
- angle brackets or ""
	- <standard stuff>
	- "your own code"
- `cout` character output
- `std` namespace
- `<<` overloaded operator
- `endl` endline
- `using` to avoid writing `std::` - temporary, we'll see later why
- be aware of namespace clashes when using `using`


### Magic Numbers and Constants

- numbers higher than 2 are "magic"
- `constexpr` constant expression
- evaluated at *compile time*
- give it a name `WORD_LENGTH`
- give it a type
- `constexpr int WORD_LENGTH = 5`


### Variables and cin for Input

- write pseudo-code
- write in comments before writing the actual code

```
// get a guess from the player

// repeat the guess back to them
```

- creating variables
- Unreal coding standard, all variable first letters are capitalized such as `string Guess = "";`
- `cin >> Guess;` take input and put it into Guess
- using the string library
- `#include string`


### Using getline()

- read through any spaces by default
- discard the input stream once it reaches the newline character
- [C++ Online Documentation](www.cplusplus.com)
- take a look at example code


### Simplifying with Functions

- Programming is all about managing complexity
- We want to think about a few things at a time
- The idea of abstraction and encapsulation
- How funcitons help us simplify
- Write and call your first functions
- A warning about "side-effects" of functions
- Always use return
- Encapsulation makes sure you adhere to your Abstraction

`void PrintIntro();`

- Function declaration at the top (**called a prototype**)
- Implementation in the body


### Iterating With For and While Loops

- "know what you're in *for*"
- "Maybe looping for a *while*"
- for (initialization; condition; increase) statement


### Clarity is Worth Fighting For

- consitent levels of abstraction
- need two methods in main
- `PrintIntro()`
- `PlayGame()`
- Right click "extract fuction" in Visual Studio
- sneakily creates a header file
- Are you happy with how your code reads?
- always have verbs in method name
- if you have to check the source code of what a method does it isn't abstracted enough


### Booleans and Comparison

- `bool AskToPlayAgain();`
- "hardest problems in coding are naming and cache validation or cache coherency"
- Right click Quick Actions "Create Definition"
- `return (Response[0] == 'y') || (Response[0] == 'Y')`
- single '' not "" when used in this comparison matters!


### Using the `do` and `while` in C++

- `do { <the code you want to repeat> } while (condition);`
- the code gets executed at least once
- prefix boolean with a small b
- `bool bWantsToPlayAgain = false;`

### Classes

- created by mathemeticians these days could be know more as types
- higher level of abstraction
- another tool for keeping only the most important things in our mind through abstraction
- generally, variables are declared private, methods that get/set the variables can be public
- Define classes in cpp files
- Declare classes in header files


### Using Header Files as Contracts

- Project -> Right Click -> Add - New Item -> Header File
- FBullCowGame - Unreal coding convention "F" prefix
- never do `using namespace` in a header file
- write what we are going to do not how

```
class FBullCowGame {
	public:
		void Reset();
		int GetMaxTries();
		int GetCurrentTry();
		bool IsGameWon();
		bool CheckGuessValidity(string);
	
	// ^^ focus on the interface above in this example ^^
	public:
	    int MyCurrentTry;
	    int MyMaxTries;
};
```


### Including our own Header File

- not including namespaces
- searchable
- remove confusion about what namespaces have been used
- search and replace `string` to `std::string`
- first create empty definitions
- Right Click Quick Actions "Create Definition"


### Instantiating your Class

- user defined type
- class is the factory
- car drives off the assembly line
- `#include "FBullCowGame.h"`
- `FBullCowGame BCGame; // instantiate`


### Writing and Using Getter Methods

- simply initialize variable initial states in the header file
- later move on to creating constructor that takes parameters
- getters at the top of header files

```
int FBullCowGame::GetMaxTries() const { return MyMaxTries; }
int FBullCowGame::GetCurrentTry() const { return MyCurrentTry; }
```


### Introducing the const Keyword

- `const` meaning depends on context
- generally means "I promise not to change this"
- `int GetCurrentTry() const;` prevents the function from modifying any member variables
- `const` in this case comes at the end of a line
- safety feature
- performed at run time
- const constexpr compile time


### Constructors for Initialisation

- computer analogy: class is the computer, when the computer comes from the factory it comes loaded with the software
- header file initialisation of member variables happens at compile time
- cpp file implementation of the constructor function initialises member variables with values at run time
- if set in both areas, constructor will ultimately set the values
- ok to call a member function or method from the constructor such as a `Reset()` that initialises values of member variables


### Pseudo-code Programming Protocol (PPP)

- planning
- `// TODO add a game summary`
- View -> Task List
- Write more in english of what you want your code to do in the future


### Using `using` for Type Aliases

- int32 - cross platform compatible, int is not
- FString & FText - fstring mutable and changeable, ftext used entirely for user output
- `using FText = std::string`
- find all std::string with FText in the main.cpp
- FText for view (the user interacts with) FString for declaration in header files and cpp implementation
- `using FString = std::string;`
- find all std::string with FString in .h
- `using` in this case is being used for a much smaller substitution not like the `std` substitution
- `using int32 = int;` int is primitive type (not in std)
- find all int and replace with int32 accept `int main()`
- repeat the int32 substitution in each file it is being used explicitely, don't just assume namespace chaining


### Using struct for Simple Types

- like a class but simpler, by default members are public
- `FBullCowCount`
- `constexpr FString HIDDEN_WORD = "planet"`
- `constexpr` too strong, cpp complains, must use `const`
- `const FString HIDDEN_WORD = "planet"`


### Using if Statements

- use `if(false)` as a temporary measure so that we can outline our function whilst keeping our code in a running state
- use switch if condition is like `if (1) {statemments}; else if (2) {statements}; ` and so on...
- PPP SubmitGuess()

```
// loop through all letters in the guess
	// compare letters against the hidden word
		// if the match
			// if they are in the same place
				// increment bulls
			// if not
				// increment cows
```


### Debugging 101

- set break point in the margin where the problem area is
- go to Debug -> Start Debugging
- Autos, Locals, and Watch tabs
- Right click -> Add Watch to watch a value


### A Place for Everything

- `HIDDEN_WORD_LENGTH`
- "A place for everything, everything in its place"
- Think carefully about what you store
- General bandwidth vs storage
- another example CPU vs RAM
- another example store birthday not age
	+ it's very easy to calculate age based on bd
- Until proven otherwise, don't store results (perf profiling)
- [data locality](http://gameprogrammingpatterns.com/data-locality.html)
- `int32 GetHiddenWordLength() const` getter
- "late binding" asking the question as late as possible


### Introduction to Enumerations

- in Unreal naming convention enums start with capital "E"
- `enum EWordStatus`

```
enum EWordStatus
{
	Invalid_Status,
	OK,
	Not_Isogram
};

enum EResetStatus
{
	No_Hidden_Word,
	OK
};

```

- If we try to compile this code we get a compile error
- "'OK': redefinition; previous definition was 'enumerator'"
- Unreal Coding standards: Strongly-Typed Enums

```
enum class EWordStatus
{
	Invalid_Status,
	OK,
	Not_Isogram
};

enum class EResetStatus
{
	No_Hidden_Word,
	OK
};

```


### Writing Error Checking Code

- use `EGuessStatus` enum to return meaningful error status instead of just `true` or `false`
- `EGuessStatus::OK, EGuessStatus::Wrong_Length, EGuessStatus::Not_Lowercase, EGuessStatus::Not_Isogram`
- rename things like `SubmitGuess` to `SubmitValidGuess` when needed to change what we perceive the funtion to do or require


### Using Switch Statements

- include break in switch statements to prevent the code in cases below from executing

```
switch (expression) // expression is what we switch based on
{
	case constant1:
		statement(s);
		break;
	case constant2:
		statement(s);
		break;
	default:
		statement(s);
}
```

- communicate to the user
- educate how to play the game
- remember break statement
- test in the console the output for wrong word length


### Warm Fuzzy Feelings

- Removing compiler warnings
- "'GetValidGuess': not all control paths return a value"
- do while loop that may keep looping to infinity
- all statements in the case statement may be jointly exhaustive (not to be confused with mutually exclusive)
- even if problem with usability is patched, a bit of refactoring and cleaning up the code is necessary to remove all potential problems and warnings
- feel good about your stuff


### Handling Game Win Condition

- finish `IsGameWon()`
- really simple, one line method implementation that just returns `bGameIsWon`


### Win or Lose Screen

- arrange a "you win / bad luck" message
- write a function for it
- write functions for the other enum statuses


### Introducing Big O Notation

   | P | L | A | N | E | T 
---|---|---|---|---|---|---
 P | x |   |   |   |   |   
---|---|---|---|---|---|---
 L |   | x |   |   |   |   
---|---|---|---|---|---|---
 A |   |   | x |   |   |   
---|---|---|---|---|---|---
 N |   |   |   | x |   |   
---|---|---|---|---|---|---
 E |   |   |   |   | x |   
---|---|---|---|---|---|---
 T |   |   |   |   |   | x 

- Sorting algorithm and `IsIsogram()`
- How many operations we need to perform?
- n = 6
- n2 - n (for the diagonal) / 2 (the area to one side of diagonal)
- (6^2 - 6)/2 = 30/2 = 15 total comparisons
- O(n^2)
- does not scale well as the problem continues
- [Wikipedia Sorting Algorithms](www.wikipedia.org/wiki/Sorting_Algorithm)
- (n log n) pretty much the fastest
- sort then check (n log n) then go through each pair (n)
	+ (n log n) + n
- `n^2 vs. (n log n) vs. n, n = 2 to 17`
- [Wolfram Alpha](https://www.wolframalpha.com/input/?i=n%5E2+vs.+(n+log+n)+vs.+n,+n+%3D+2+to+17)
- Look at the performance of these three algorithms `n`, `n^2` and `(n log n)`
- what algorithm is best for `IsIsogram()`
	+ hash table?
	+ O(n)

- BOOM

	 L | X 
	-------
	 A | 0 
	 B | 1 
	 C | 0 
	 D | 0 
	 E | 0 
	 F | 0 
	 G | 0 
	 H | 0 
	 I | 0 
	 J | 0 
	 K | 0 
	 L | 0 
	 M | 0
	 N | 0
	 O | 2 <- DUPLICATE


### `TMap` and `std::map` Data Structure

- `#define TMap std::map` keep it "Unreal"
- `TMap<char, bool> LetterSeen;` to declare
- `LetterSeen[Letter]` return bool
- [UE4 Libraries|Common Containers](https://www.unrealengine.com/en-US/blog/ue4-libraries-you-should-know-about)
- How we are using a map
- hApPy as an example

	key        | value | note
	----------------------------------
	h          | true  |     
	a (from A) | true  |     
	p          | true  |     
	p (from P) | true  | return false;

- [std::map](http://www.cplusplus.com/reference/map/map/)
- [UE TMap](https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/TMap/)
- `#include <map>`
- `#define identifier replacement` - preprocessor directive
	+ `#define TMap std::map`
- literally like cut and paste

### Range-based for Loop

- containers and iterators
- range-based for loop
- `auto` keyword
- `IsIsogram()`
- `std::unordered_set` or Unreal `TSet` are alternatives that can be used here
- interface similar to that of a standard container
- `for (auto Letter : Word)  // For all letters in word`
- `auto` is used here instead of `char`


### Design a Helper Function

- `IsLowercase()`
- range-based for loop
- `auto` keyword
- handle strings of zero length `\0`
- `islower` method
- F.A.I.L (from adversity I learn)

- realize the order of `if` statements matter in `CheckGuessValidity()`
- Implicit
	+ not directly expressed
	+ suggested
- Dependent
	+ reliant on something else


### Playtesting our Game

- 3rd party
- record screen
- go fix obvious bugs
- repeat until bug/issue rate plateaus


### Difficulty and Play Tuning

- google flow channel
- [Flow Channel](https://duckduckgo.com/?q=flow+channel&atb=v40-3bs&iax=images&ia=images)
- change the word, change the number of tries
- use another TMap to map HiddenWord.length() to max tries for scaling the difficulty
- `TMap<int32, int32> WordLengthToMaxTries{{3,5}, {4,5}, {5,5}, {6,5}}`


### Polishing and Packaging

- first impressions
- think reviews
- first reviews are most important
- ship to customers
- comment with "why"
- introduce classes (block quote)
- #pragma once at the top of each file
- TODOs cleared
