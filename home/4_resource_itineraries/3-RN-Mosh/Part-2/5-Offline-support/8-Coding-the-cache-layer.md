# 8. Coding the cache layer
Created Sat Dec 30, 2023 at 1:55 PM

- The layer is just a set of 4 CRUD functions.
	  1. set - add timestamps, serialize, insert with into AsyncStorage.
	  2. get - de-serialize and return object. if time is past some predefined TTL, delete the entry from storage and return null.
	  3. update - like set
	  4. delete - well just delete
- We'll add a constant `cache-` prefix to all keys here, since we may use AsyncStorage for other things too, that are unrelated to caching
