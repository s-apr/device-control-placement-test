For compilation:
I used g++ to compile and test the program: "g++ -std=c++20 main.cpp -o device_control"

Task breakdown:
I broke each task down into smaller parts, starting with;
	1. Find and fix problems
	- Initial approach meant running the program and seeing what errors occur
	- First errors encountered were missing headers
		- added <iostream> & <algorithm>
			- <iostream> for input & output, <algorithm> to solve listeners.erase error (::remove) not a member of (::ranges)
	- Second errors were syntax, when the test set preamp levels; (-6) when expecting (-66)
		- simple text change
	- Third problem was with 'set-preamp-level' when entering no value, instead of providing
	  an error message the program would crash.
		- added if statement to check if the input value is empty, and to return nullopt
		- this now gives an error message instead of crashing
	- At this point, I put the .cpp into Claude.ai to see what other problems/fixes could be identified
	  it suggested EOF Handling (I don't know what this concept is so have ignored it), and several other
	  general user interface suggestions which don't effect the overall program at runtime.
	
	2. Add set/get "phantom power"
	- Create Boolean member variable for on/off
		- "bool phantomPowerEnabled = false"
	- Create set/get methods
		- Setter method passes a bool argument 'enable' to control the phantom power
			- phantomPowerEnabled is set to either true or false with 'enable'
			- The notifyListener() method is used to output any changes made to the console
		- Getter method is used to return the value of private member variable
			- It is only used when querying the program for 'status'.

	3. Add pre-amp value range checking
	- Simple if statements comparing the declared constants in the Device class (MINUS_INFINITY_DB & UNITY_GAIN_DB)
          to the value entered (and converted by stoi).
		- Try and Catch are used to ensure no non-integer characters can be entered
			- If statements are NOT used due to all the possible checking that would need to be done for invalid inputs

Resources used:
	- Google
	- Stackoverflow
	- Claude.ai