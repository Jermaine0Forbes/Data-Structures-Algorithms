# Arrays

- [exclude dates if they intersect][dates-intersect]

[home]:#arrays
[dates-intersect]:#excludes-dates-if-they-intersect


### exclude dates if they intersect 

<details>
<summary>
View Content
</summary>

 :dizzy_face: **Problem:**  There's an array of different dates that start and end. You are supposed to only include dates that do not intersect each other.
---
:open_mouth: Explanation: There's an array or maybe even a dictionary of different start and end date values. The solution is to have an array that collect all the unique date ranges, compare a new date range to an already verified date range, and if the new date range is not intersecting the existing unique date range then you will also store new date range into the array that has the unique date ranges. To verify if a date range is unique you would need to loop through original array, convert the start and end dates to milliseconds and compare them to each unique date range. This will essentially be the comparison

```	
	isIntersecting = (uniqueStartDate <= newStartDate and newStartDate <= uniqueEndDate)
	or ( uniqueStartDate <= newEndDate  and newEndDate <= uniqueEndDate)
	or (uniqueStartDate >=  newStartDate and newEndDate >= uniqueEndDate);
``` 
this is the core logic to tell the difference in terms of dates intersecting each other

- [php solution][php-1]
- [c# solution][cs-1]
- [python solution][py-1]
- [javascript solution][js-1]

  [php-1]:#php-solution
  [cs-1]:#cs-solution
  [py-1]:#python-solution
  [js-1]:#javascript-solution

  #### javascript solution

```js
console.log('hello world')
```
  
  #### python solution

```python
print('hello world')
```

  #### cs solution

```cs
Console.WriteLine('hello world')
```
  
  #### php solution

```php
	<?php
	const DEBUG = true;

	# the assortment of date ranges
	$allDatesArray = [
		["start_date" => "2026-01-26", "end_date" => "2026-01-29"],
		["start_date" => "2026-02-13", "end_date" => "2026-02-18"],
		["start_date" => "2026-01-14", "end_date" => "2026-01-29"], # this date range intersects
		["start_date" => "2026-02-01", "end_date" => "2026-02-04"],
		["start_date" => "2026-02-20", "end_date" => "2026-02-24"], 
		["start_date" => "2026-02-01", "end_date" => "2026-02-04"], # this date range intersects
		["start_date" => "2026-03-01", "end_date" => "2026-03-04"],
		["start_date" => "2026-01-01", "end_date" => "2026-04-06"], # this date range intersects
		["start_date" => "2026-04-01", "end_date" => "2026-04-06"],
		];
		

	# This is primarily here for line breaking
	function br (): void 
	{
		echo "\n";
	}

	# returns a date string in milliseconds
	function getMilliseconds(string $date): int
	{
		return (int)(new DateTime($date))->format('Uv');
	}

	# assigns getMilliseconds the function to a variable
	$gm =  'getMilliseconds';

	/*
	$arr = [
		'start_date' => '3-1-26',
		'end_date' => '3-4-26'
	]
	Retrieves the values from start_date and end_date,
	turns the dates into milliseconds, 
	then returns an array of those millisecond dates
	*/
	function  getMillisecondsDate (array $arr) 
	{
		global $gm;
		list($startMilliseconds, $endMilliseconds) =  array_map(fn($date):int => $gm($date), array_values($arr) );

		return [
			$startMilliseconds,
			$endMilliseconds
		];
	}

	# assigns getMillisecondsDate the function to a variable
	$gmd = 'getMillisecondsDate';


	/*
		Checks to see if the current date range 
		is intersecting an existing date range
	*/
	function checkRange(array $current, array $exist) : bool
	{
		global $gmd;

		list($cStart, $cEnd) = $gmd($current);
		list($eStart, $eEnd) = $gmd($exist);
		$cs = $current['start_date'];
		$es = $exist['start_date'];
		$ce = $current['end_date'];
		$ee = $exist['end_date'];
		
		$currentStartDateIntersects = ($eStart <= $cStart && $cStart <= $eEnd);
		$currentEndDateIntersects =  ( $eStart <= $cEnd  && $cEnd <= $eEnd);
		$currentDatesOverlap = ($eStart >=  $cStart && $cEnd >= $eEnd);

		$intersects =  $currentStartDateIntersects|| $currentEndDateIntersects || $currentDatesOverlap;
		$result = $intersects ? "true" : "false";

		if(DEBUG) {
			echo "Is $cs - $ce  intersecting $es - $ee? ".$result;
			br();
		}
		
		return  $intersects;
	}

	$uniqueDatesArray = [];

	/*
	Loops through the array of date ranges
	and only stores them to the $uniqueDatesArray variable
	if it is the first date range or any of the
	current date ranges do intersect the existing
	date ranges that are inside $uniqueDatesArray
	*/
	for($i  = 0 ; $i < sizeof($allDatesArray); $i++) {
		
		$recentDateRange = $allDatesArray[$i];
		list($recentStart, $recentEnd) = $gmd($recentDateRange);
		
		if(DEBUG) {
			echo "this should be the start date: $recentStart and end date: $recentEnd, for the recent date range";
			br();
		}

		$isUnique = true;

		/* if this is the first date range
		then store it, and go to the next iteration
		*/
		if($i === 0 ) {
			$uniqueDatesArray[] = $recentDateRange;
			if(DEBUG){
				echo "first unique date entry";
				br();
				br();
			}
			continue;
		}

		foreach( $uniqueDatesArray as $k => $uniqueDateRange) {
			if(DEBUG){
				br();
				echo "unique date entry: ".($k+1);
			}

			list($uniqueStart, $uniqueEnd) = $gmd($uniqueDateRange);

			if(DEBUG){
				br();
				echo "this unique date is between $uniqueStart - $uniqueEnd and its average is ".($uniqueStart+$uniqueEnd)/2;
				br();
				echo "current date shows $recentStart - $recentEnd and it's average is ".($recentStart+$recentEnd)/2;
				br();
			}
		
			if(checkRange($recentDateRange, $uniqueDateRange)){
			$isUnique = false;
			break;
			}

		}
		if(DEBUG){
			br();
		}
		
		if($isUnique){
			$uniqueDatesArray[] = $recentDateRange;
		}

	}

	var_dump($uniqueDatesArray);

```




</details>

[go back to table of contents][home]



