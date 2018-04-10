# Mummipy

Preserve your requirements forever!

Bundles a loosely specified python requirements.txt into a tarball.
The entombed requirements have everything you need for offline reproducible builds.

# Mummipy file format

The mummipy format is simply a gzipped tarball.

It contains ./requirements.txt with sha256 hashes added and  containing all package tarballs at ./tomb/.

# Example

```
$ cat requirements.txt
pyYAML

# create a mummipy archive
$ mummipy -r ./requirements.txt -o requirements.mummipy

# create a venv from the mummipy archive
$ unmummipy -r requirements.mummipy -o ./venv
...
$ ./venv/bin/python
>>> import yaml
>>>

# List the contents of the mummipy
$ tar tfz requirements.mummipy
./
./tomb/
./tomb/PyYAML-3.12.tar.gz
./requirements.txt

# List the enclosed hashes

$ unmummipy -r requirements.mummipy -l

PyYAML==3.12  --hash=sha256:592766c6303207a20efc445587778322d7f73b161bd994f227adaa341ba212ab

```

# Limitations

- Does not use binary packages.
- Does not support windows.
- Only supports python3.

# Benefits

- It exists, whoever wrote pip doesn't care about reproducible builds.
