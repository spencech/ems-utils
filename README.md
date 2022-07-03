# EMS Utils
Utility methods that are frequently used in Educational Media Solutions web applications.

# Methods

## alphabetize(...parameters: any[]): any
Can be used as the callback argument to Array.sort

	(["e","a","c", "d", "b"]).sort(alphabetize); // ["a", "b", "c", "d", "e"]

Also can be used to alphabetize array of objects using key (note: this method mutates original array)

	alphabetize([{"label": "b"}, { "label": "a" }], "label"); //[{ "label": "a" }, {"label": "b"}]

## clone(obj: any): any
Creates a deep copy of the supplied object. References are not maintained. Recursion not supported.

	const copy = clone({hello: [{ nested: "object", params: [1,2,3] }]}); //{hello: [{ nested: "object", params: [1,2,3] }]}

## dateStrings(date?: Date): { year: string, month: string, date: string, time: string seconds: string }
Returns a hash of dates properties as strings (for formatting)

	const dateinfo = dateStrings(new Date("2021/01/01")); { year: "2021", "month": "01", "date": "01", "time": "00:00", "seconds": "00" }

## delay(method: () => void, ms: number = 0): number
Alias for window.setTimeout

	delay(() => console.log("test")); // same as window.setTimeout(() => console.log("test"), 0);
	delay(() => console.log("test"),100); // same as window.setTimeout(() => console.log("test"), 100);

## download(content: string, name: string, extension: string = "csv"):void
Downloads in memory string as file (in web browser)

	download("header 1,header 2\nvalue 1, value 2\nvalue 3, value 4","Sample Spreadseet", "csv"); //outputs: "sample-spreadsheet.csv" as CSV file

## empty(e: any): boolean
	alias for falsy

## falsy(e: any): boolean
Evaluates whether supplied object is falsy or empty

	const obj = {}; falsy(obj); //true
	const obj = {hello: "world"}; falsy(obj); //false
	const arr = []; falsy(arr); //true
	const arr = [1,2,3]; falsy(arr); //false
	const str = ""; falsy(str); //true
	const str = "   "; falsy(str); //true
	const str = "hello"; falsy(str); //false
	const bool = false; falsy(bool); //true
	const bool = true; falsy(bool); //false
	const boolString = "False"; falsy(boolString); //true
	const boolString = "false"; falsy(boolString); //true
	const boolString = "FalSe"; falsy(boolString); //true
	const boolString = "true"; falsy(boolString); //false
	const num = 0; falsy(num); //true
	const num = -1; falsy(num); //false
	const num = 1; falsy(num); //false

## focus(selector: string): number
Sets browser focus on supplied element

	const $button = $("body").add("<button>Focus Me</button>");
	focus($button); //focuses button after one turn of JS engine

## getLargestRemainder(values: number[], desiredSum: number): number[]
Handles rounding errors when calculating sub percentages of a data set. Ensures that all segments add up to 100%.

	getLargestRemainder([24, 25, 50]); // [25,25,50]

## getparams(requestedProperty?: string): any
Returns get parameters from the browser url

	getparams(); // { debug: true, userId: 1, hello: "world" } where http://localhost/?debug=true&userId=1&hello=world
	getparams("hello"); // "world" where http://localhost/?debug=true&userId=1&hello=world

## isset(e: any): boolean
	alias for truthy

## kebab(e: string): string
Converts string to kebab case

	kebab("Hello Big_World 2022-01-01"); // "hello-big-world-2022-01-01"

## replaceItem(array: any[], item: any, key: string = 'id', position: string = 'current'): any
Swaps an item in an array with a newer value

	const array = [ { id: 1, name: "Old Name" }, { id: 2, name: "Test User" }];
	replaceItem(array, {id: 1, name: "New Name"}); // [ { id: 1, name: "New Name" }, { id: 2, name: "Test User" }]

	const array2 = [ { id: 1, name: "Old Name" }, { id: 2, name: "Test User" }];
	replaceItem(array, { id: 200, name: "Test User" }, "name"); // [ { id: 1, name: "Old Name" }, { id: 200, name: "Test User" }]

## snakecase(e: string): string
Converts string to snake case

	snakecase("Hello Big-World 2022-01-01"); // "hello_big_world_2022_01_01"

## tick(returnValue?: any): Promise<any>
Awaits one turn of the JS engine

	async function test() {
		$(".torender").css("display","block").addClass("transparent"); //renders the object on screen with 0 opactiy
		await tick(); // browser tick paints the above state
		$(".torender").removeClass("transparent); //animates opacity to 1 to fade in object
	}

## timestamp(date?: Date, includeTime: boolean = true): string
Returns MySQL date/time string from optionally supplied date

	const date = new Date("2021/01/01"); 
	const dateString = timestamp(date); // "2021-01-01 00:00:00";
	const dateString2 = timestamp(date, false); // "2021-01-01";
	const nowDateString = timestamp(); // whateve the current date time is

## trace(...parameters: any[])
Outputs each argument to a line in console log

	trace(someObject, anotherObject, "---", 123); //four console logs

## trim(e: string): string
Removes leading and trailing whitespace from string

	trim("  hello   "); // "hello"

## truthy(e:any): boolean
Evaluates whether supplied object is truthy or populated

	const obj = {}; truthy(obj); //false
	const obj = {hello: "world"}; truthy(obj); //true
	const arr = []; truthy(arr); //false
	const arr = [1,2,3]; truthy(arr); //true
	const str = ""; truthy(str); //false
	const str = "   "; truthy(str); //false
	const str = "hello"; truthy(str); //true
	const bool = false; truthy(bool); //false
	const bool = true; truthy(bool); //true
	const boolString = "False"; truthy(boolString); //false
	const boolString = "false"; truthy(boolString); //false
	const boolString = "FalSe"; truthy(boolString); //false
	const boolString = "true"; truthy(boolString); //true
	const num = 0; truthy(num); //false
	const num = -1; truthy(num); //true
	const num = 1; truthy(num); //true

## validateEmail(email:string): boolean
Applies regex to test for valid email

	validateEmail("test@test"); //false
	validateEmail("test@test.co"); //true

## viewport(el: HTMLElement, percentVisible: number = 100): boolean
Determines whether the supplied object is within the browser's viewport

	const inRangeElement = $(".block.inview").get(0);
	const outOfRangeElement = $(".block.waydownbelow").get(0);
	let inView = viewport(inRangeElement); // true;
	inView = viewport(outOfRangeElement); // false

# Build
	npm run build
	git commit -a -m "message"
	npm version patch
	npm publish