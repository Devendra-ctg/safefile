# safefile

[![Build Status](https://travis-ci.org/dchest/safefile.svg)](https://travis-ci.org/dchest/safefile)

Go package safefile implements safe "atomic" saving of files.

Instead of truncating and overwriting the destination file, it creates a
temporary file in the same directory, writes to it, and then renames the
temporary file to the original name when calling Commit.

## Installation

```
$ go get github.com/dchest/safefile
```

## Documentation
	
 <http://godoc.org/github.com/dchest/safefile>

## Example

```go
f, err := safefile.Create("/home/ken/report.txt")
if err != nil {
	// ...
}
// Created temporary file /home/ken/sf-ppcyksu5hyw2mfec.tmp

defer f.Close()

_, err = io.WriteString(f, "Hello world")
if err != nil {
	// ...
}
// Wrote "Hello world" to /home/ken/sf-ppcyksu5hyw2mfec.tmp

err = f.Commit()
if err != nil {
    // ...
}
// Renamed /home/ken/sf-ppcyksu5hyw2mfec.tmp to /home/ken/report.txt
```
