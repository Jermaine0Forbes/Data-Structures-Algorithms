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
// Enter your code here, enjoy!
$array = [
	 ["start_date" => "2026-01-26", "end_date" => "2026-01-29"],
	 ["start_date" => "2026-02-13", "end_date" => "2026-02-18"],
	 ["start_date" => "2026-01-14", "end_date" => "2026-01-29"],
	 ["start_date" => "2026-02-01", "end_date" => "2026-02-04"],
 	 ["start_date" => "2026-02-20", "end_date" => "2026-02-24"],
  	 ["start_date" => "2026-02-01", "end_date" => "2026-02-04"],
   	 ["start_date" => "2026-03-01", "end_date" => "2026-03-04"],
   	 ["start_date" => "2026-01-01", "end_date" => "2026-04-06"],
   	 ["start_date" => "2026-04-01", "end_date" => "2026-04-06"],
	];
	
$f = "Y-m-d";
$m = "+5 days";

function br () {
	echo "\n";
}

function getMills(string $date)
{
	return (new DateTime($date))->format('Uv');
}

function checkRange($current, $exist) {
	$cs = $current['start_date'];
	$es = $exist['start_date'];
	$cStart = (int)getMills($cs);
	$eStart = (int)getMills($es);
	
	
	$ce = $current['end_date'];
	$ee = $exist['end_date'];
	$cEnd = (int)getMills($ce);
	$eEnd = (int)getMills($ee);
	
	$result = ($eStart <= $cStart && $cStart <= $eEnd) || ( $eStart <= $cEnd  && $cEnd <= $eEnd) || ($eStart >=  $cStart && $cEnd >= $eEnd);
	br();
	echo "Is $cs - $ce  intersecting $es - $ee? ". (bool)$result;
	br();
	
	return  $result;
}

br();
	
$d =  new DateTime();
// echo $d->modify($m)->format($f);

br();
$dateArr = [];

for($i  = 0 ; $i < sizeof($array); $i++) {
	
	$range = $array[$i];
	$start = (int)getMills($range['start_date']);
	$end = (int)getMills($range['end_date']);
	$overlap = true;
	//echo $start;
	if($i === 0 ) {
		$dateArr[] = $range;
		continue;
	}
	foreach( $dateArr as $k => $v) {
		echo "the ".($k+1)." date entry";
		$s = (int)getMills($v['start_date']);
		$e = (int)getMills($v['end_date']);
		
		/*
		br();
		
		echo "is between $s - $e and its average is ".($s+$e)/2;
		br();
		
		echo "current date shows $start - $end and its average is ".($start+$end)/2;
		br();
		
		*/
	
		if(checkRange($range, $v)){
		 $overlap = false;
          break;
		}

	}
	br();
	
	if($overlap){
		$dateArr[] = $range;
	}

}
```

Explanation: 

</details>

[go back to table of contents][home]



