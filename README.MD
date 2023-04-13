# What is the story with printing every step?

I have raised a question about preinting every build step,
while building executable with Ninja.

It seems that adding printf " " before actual command force Ninja to
print description for build step and **not erase this text after step is finished**.

But maybe there is a some better way to do this.

