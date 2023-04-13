# What is the story with printing every step?

I have raised a question about preinting every build step,
while building executable with Ninja:

https://stackoverflow.com/questions/76005072/using-build-ninja-and-expecting-printing-descriptions-of-the-steps-when-build

It seems that adding printf " " before actual command force Ninja to
print description for build step and **not erase this text after step is finished**.

So this:
```
# RULES
rule compile
  description = Compiling $in to the $out...
  command = printf " " && $cc $cflags -c $in -o $out

rule link
  description = Linking $in to the $out...  
  command = printf " " && $cc $ldflags $in -o $out

rule clean
  description = Removing $target.o...
  command = printf "" && rm -f $target.o
  ```
  
  Give me this:
```
$ ninja
[1/3] Compiling main.c to the helloProgram.o...
[2/3] Linking helloProgram.o to the helloProgram...  
[3/3] Removing helloProgram.o...
```

**NOTE**: I use printf "" && ... and not printf " " && ... in the last command.

This output shows me all the information I need, and such aproach could be scaled to the larger projects.

But maybe there is a some better way to do this.

