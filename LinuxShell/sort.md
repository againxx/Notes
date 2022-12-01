# Sort

* `-n` compare according to string numerical value
* `-k KEYDEF` sort via a key, *KEYDEF* gives location and type

**KEYDEF** is of the form `F[.C][OPTS][,F[.C][OPTS]]` for start and stop position,
where F is a field number and C a character position in the field; both are defaults to 1,
and the stop position defaults to the line's end. OPTS can be ordering options
