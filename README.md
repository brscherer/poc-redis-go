# Redis Clone - GO

We'll use same port that redis, so first thing is to stop redis:

```brew services stop redis```

Running server:

`go run *.go`
`redis-cli`


## RESP (Redis Serialization Protocol)

`*3` - indicates that we have an array with a size of 3. It means it will read 6 lines. Each pair of line represents type and size of object. second line contains the value of that object
`$5` - indicates its string with length of 5. next line will contain exatcly 5 characters.

## Handling IO (Bufio)

Bufio has methods that makes easier to work with data, such ReadLine and ReadByte

```$5\r\nBruno\r\n```

1. Read Byte - `$`
2. Read Number - `5`
3. Read Byte - `\r`
4. Read Byte - `\n`
...

## Handling concurrency

RWMutex is used to avoid multiple threads writing in same map for SET and HSET commands.

Everytime we try to SET a new value, we use LOCK to avoid other threads to modify the map we are currently using.

Then we write the value and UNLOCK it so next time we try to set, the process is repeated.

## Persisting Data

Using AOF, we'll record each command in the file as RESP. When server restart, we'll read all the RESP commands from the AOF file and execute them in memory