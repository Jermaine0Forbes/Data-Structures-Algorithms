# Arrays

- [exclude dates if they intersect][dates-intersect]

[home]:#arrays
[dates-intersect]:#excludes-dates-if-they-intersect


### exclude dates if they intersect 

<details>
<summary>
View Content
</summary>

**Problem:**  There's an array of different dates that start and end. You are supposed to only include dates that do not intersect each other.
---

:exclamation: **Note:**

---

```php
<?php


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
function getMills(string $date): int
{
	return (int)(new DateTime($date))->format('Uv');
}

/*
	Checks to see if the current date range 
	is intersecting an existing date range
*/
function checkRange(array $current, array $exist) : bool
{
	$cs = $current['start_date'];
	$es = $exist['start_date'];
	$cStart = getMills($cs);
	$eStart = getMills($es);
	
	
	$ce = $current['end_date'];
	$ee = $exist['end_date'];
	$cEnd = getMills($ce);
	$eEnd = getMills($ee);
	
	$intersects = ($eStart <= $cStart && $cStart <= $eEnd) || ( $eStart <= $cEnd  && $cEnd <= $eEnd) || ($eStart >=  $cStart && $cEnd >= $eEnd);
	$result = $intersects ? "true" : "false";
	br();
	echo "Is $cs - $ce  intersecting $es - $ee? ".$result;
	br();
	
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
	$start = getMills($recentDateRange['start_date']);
	$end = getMills($recentDateRange['end_date']);
    list($st, $en) =  array_map(fn($date):int => getMills($date), array_values($recentDateRange) );
    echo "this should be the start: $st and end: $en ,  for the recent date range";
    br();

	$isUnique = true;

    /* if this is the first date range
       then store it, and go to the next iteration
    */
	if($i === 0 ) {
		$uniqueDatesArray[] = $recentDateRange;
		continue;
	}

	foreach( $uniqueDatesArray as $k => $uniqueDateRange) {
		echo "the ".($k+1)." date entry";
		$s = getMills($uniqueDateRange['start_date']);
		$e = getMills($uniqueDateRange['end_date']);
		
		/*
		br();
		
		echo "is between $s - $e and its average is ".($s+$e)/2;
		br();
		
		echo "current date shows $start - $end and its average is ".($start+$end)/2;
		br();
		
		*/
	
		if(checkRange($recentDateRange, $uniqueDateRange)){
		 $isUnique = false;
          break;
		}

	}
	br();
	
	if($isUnique){
		$uniqueDatesArray[] = $recentDateRange;
	}

}

var_dump($uniqueDatesArray);

```

Explanation: 

</details>

[go back to table of contents][home]



