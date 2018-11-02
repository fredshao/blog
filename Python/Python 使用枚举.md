## Python 使用枚举

```python
from enum import IntEnum

class TripSource(IntEum):
	FROM_WEBSITE = 11
	FROM_IOS_CLIENT = 12

def mark_trip_as_freatured(trip):
	if trip.source == TripSource.FROM_WEBSITE:
		do_some_thing(trip)
	elif trip.source == TripSource.FROM_IOS_CLIENT:
		do_some_other_thing(trip)
```

