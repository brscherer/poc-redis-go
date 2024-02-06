# Redis Clone - GO

We'll use same port that redis, so first thing is to stop redis:

```brew services stop redis```


# RESP (Redis Serialization Protocol)

`*3` - indicates that we have an array with a size of 3. It means it will read 6 lines. Each pair of line represents type and size of object. second line contains the value of that object
`$5` - indicates its string with length of 5. next line will contain exatcly 5 characters.