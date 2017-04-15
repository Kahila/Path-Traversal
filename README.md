# Path-Traversal
Path Traversal Tips


1. Always try path traversal sequences using both forward slashes and backslashes.
Many input filters check for only one of these, when the filesystem
may support both.
 2. Try simple URL-encoded representations of traversal sequences using the
following encodings. Be sure to encode every single slash and dot within
your input:
Dot — %2e
Forward slash — %2f
Backslash — %5c
3. Try using 16-bit Unicode encoding:
Dot — %u002e
Forward slash — %u2215
Backslash — %u2216
4. Try double URL encoding:
Dot — %252e
Forward slash — %252f
Backslash — %255c
5. Try overlong UTF-8 Unicode encoding:
Dot — %c0%2e, %e0%40%ae, %c0ae, and so on
Forward slash — %c0%af, %e0%80%af, %c0%2f, and so on
Backslash — %c0%5c, %c0%80%5c, and so on
You can use the illegal Unicode payload type within Burp Intruder to
generate a huge number of alternate representations of any given character
and submit this at the relevant place within your target parameter.
These representations strictly violate the rules for Unicode representation
but nevertheless are accepted by many implementations of Unicode
decoders, particularly on the Windows platform.
 6. If the application is attempting to sanitize user input by removing traversal
sequences and does not apply this filter recursively, it may be
possible to bypass the filter by placing one sequence within another. For
example:
....//
....\/
..../\
....\\
