# Why is a newline needed at the end of a github file?
`#GitHub` `#Newline` `#POSIX` `#Incomplete_Line`

## ✓ Trigger
![img](https://github.com/celestedayoung/TIL/assets/144453750/def2fda7-351c-4c6c-9eb3-666e5186c0cf)  
While surfing the internet, i came across an article mentioning that `GitHub gives a warning if a file doesn't have a newline character at the end`. Reading this made me realize that there always been a newline character at the end of my code, and I became curious about its significance, prompting me to look it up.

## ✓ What is a newline?

### Newline
> A newline(frequently called line ending, end of line(EOL), next line(NEL) or line break) is a control character or sequence of control characters in character encoding specifications such as ASCII, Unicode, etc.
- This character, or a sequence of characters, is used to **signify the end of a line of text and the start of a new one**.
  
## ✓ Warning: No newline at end of file

- The last line of a file should include a newline character, as this is required to comply with POSIX.
- While the absence of a newline character may not pose an immediate issue, it can potentially lead to problems in the future, which is warrants a warning.

### POSIX
> The Portable Operating System Interface is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems.
- POSIX defines both the system and user-level application programming interfaces(APIs), along with command line shells and utility interfaces, for software compatibility with variants of Unixd other operating systems.


## ✓ Why is a newline needed at the end of a file?

### 3.195 Incomplete Line
> A sequence of one or more non-`<newline>`characters at the end of the file.

### 3.206 Line
> A sequence of zero or more non-`<newline>`characters plus a terminatng <newline> character.

- According the above definitions, a line is considered complete only if it includes a newline character at the end.
- Otherwise, it may still be interpreted as an ongoing line, potentially leading to failure in recognizing whether the current position is at the end of the file.

---
### references
https://en.wikipedia.org/wiki/POSIX  
https://en.wikipedia.org/wiki/Newline  
https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline  
https://stackoverflow.com/questions/5813311/whats-the-significance-of-the-no-newline-at-end-of-file-log  
https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_206  
https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_195  
https://hyeon9mak.github.io/github-no-newline-at-a-end-of-file