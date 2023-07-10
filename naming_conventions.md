# NAMING CONVENTIONS

This section describes recommendations for naming conventions.

## MANDATORY

### Name Shadowing

**Description:** Functions and variables shall not shadow Mathworks-shipped functionality or other code. This includes MATLAB files (.m, .p, .mlapp, .mlx), mex-files (.mexw32 etc.) and Simulink files (.mdl, .slx).

**Rationale:** Shadowing code can result in unexpected behaviour, because it is unclear and not properly defined for example what function is called when multiple ones share the same name.

### Units

**Description:** Variable names must be documented, either in the variable name, or as end-of-line comments in square brackets. Prefer end-of-line comments if addition to the variable name will make it excessively long.

**Rationale:** Maintain readability by using concise variable names.

DO:

	time_min = 2; 
	time_s = 120; 
	acceleration = 1000; % [mm/s^2] 
	
DON'T:

	time = 2; 
	accelerationInMillimetersPerSecondSquared = 1000;
	
	

## STRONGLY RECOMMEND

### Negated Boolean Names

**Description:** Avoid variable names including the word not.

**Rationale:** Readability decreases when variables have negated boolean names, especially in combination with the ~ operator.

DO:

	if isValid && ~isFound 
    	error('My error message.') 
	end 

DON'T:

	if ~notValid && isNotFound 
		error('My error message.') 
	end 
	
### Descriptive Names

**Description:** Use precise and descriptive names for functions, classes,
packages and variables.

**Rationale:** This increases the readability of the code.

DO:

	function tk = convC2k(temp)
	
DON'T:

	function temperatureK = convertCelsiusToKelvin(temperatureC) 
	
	
### The 'n' Prefix

**Description:** The prefix n should be used for variables that represent a number of things. Do not use the prefix for other purposes and do not use other prefixes for representing the number of things.
**Rationale:** Variables starting with this prefix can easily be identified.

DO:

	nFiles 
	nCars 
	nLines 
	
DON'T:

	numberOfFiles 
	nrCars 
	lineCount

## BEST PRACTICES

### Name Length

**Description:** Variable names shall be at most 32 characters long. Function names shall be at least 3 and at most 32 characters long.

**Rationale:** Names shall be descriptive, so should not be too short. However, variable names can sometimes be single characters (x, y) and still be descriptive. Names that are too long can reduce readability because they introduce long lines of code.

DO:
	
	maxData = max(data); 
    

DON'T

    maximumValueOfTheEntireSetOfDataPoints = max(data);

### Loop Iterator Naming

**Description:** Iterator variable names shall be at least 3 characters long. In nested for-loops, the starting letters of the iterator names shall be subsequent letters in the alphabet.

**Rationale:** Iterator variables of for-loops are easily distinguishable from other variables by using these prefixes.

DO:

	for iNode = 1 : 10 
		for jPoint = 1 : 3 
       	myGraph(iNode).plotIt(jPoint); 
    	end 
	end 

DON'T:

	for nodeIdx = 1 : 10 
    	for j = 1 : 3 
       	myGraph(nodeIdx).plotIt(j); 
    	end 
	end   

### Parent / Child Name Redundancy

**Description:** Names of fields and properties shall not contain their parent struct or object's name.
**Rationale:** When referenced, the fields and properties can have the same phrase multiple times in a row, which is unnecessary.

DO:

	Beam.thickness 
	chair.weight 

DON'T:

	Beam.beamThickness 
	chair.weightOfChair
	

### Names to Avoid

**Description:** Names of classes, functions, variables, properties and struct fields should not start with temp, my and they should not have names such as myClass, testFunction, etc.

**Rationale:** Names like these do not properly indicate what the class, function or variable is for.

In particular: 

	myClass 
	my_Class 
	TheClass 
	myFunction 
	myFunc 
	my_function 
	TheFunc 
	myVar 
	my_var 
	theVar 
	myProp 
	my_prop 
	temp 
	tmp 
	test 
	
### Function Names Document Their Use

**Description:** The names of functions should document their use.

**Rationale:** By choosing a clear and descriptive name, the code becomes more readable.

DO:

	model_rMatGet 
	control_bpmGet 
	util_gaussFit 
	gui_sliderControl  

DON'T:

	modelFunction 

### Function Name Construction

**Description:** All function names shall consist of a verb and a noun. When appropriate also include a grouping (model\_, control\_, util\_, gui\_, etc.)

**Rationale:** This way it is more likely to be clear what the function does and if there is no suitable name following this guideline, (for example because the function does more than one thing) the function may have to be refactored.

DO:

	model_rMatGet 
	control_bpmGet 
	util_gaussFit 
	gui_sliderControl  
	do_thing 

DON'T:

	rMat 
	gauss 
	bpms 
	sliderstuff 


### Casing

TBD


### The 'is' Prefix

**Description:** The is prefix shall be used for functions returning logical values or properties and variables holding logical values.

**Rationale:** This increases the readability of the code as it is clear from the name.


### Abbreviations

**Description:** Variable names shall not contain abbreviations; except for idiomatic abbreviations commonly used at SLAC. (Found in SLAC Speak)

**Rationale:** Maintain readability by not abbreviating words in your variable names. Common acronyms are allowed.

DO:

	arrivalTime 
	bpmCharge 
 
COMMON EXCEPTIONS: 

	bpm 
	toro 
	xcor 
	ycor 
	bdes 
	
DON'T:

	arrTim 
	bpmC
	
	
### The 'Test' Suffix

**Description:** Use the suffix Test only for unit test filenames.

**Rationale:** This increases the readability of the code as it is clear from the name of the file that it is a unit test file.
