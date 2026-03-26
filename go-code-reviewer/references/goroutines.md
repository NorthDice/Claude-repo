# Goroutines & Concurrency

## Goroutine leaks

Goroutine started but never stopped.

```go
// BAD — leaks if nobody reads ch
go func() {
    ch <- result
}()

// GOOD — respect context cancellation
go func(ctx context.Context) {
    select {
    case ch <- result:
    case <-ctx.Done():
    }
}(ctx)
```

Loop variable capture (pre-Go 1.22):
```go
// BAD — all goroutines share same v
for _, v := range items {
    go func() { process(v) }()
}

// GOOD
for _, v := range items {
    v := v
    go func() { process(v) }()
}
```

## Data races

- Shared variable written from multiple goroutines without mutex or atomic
- Map read/write from multiple goroutines — always use `sync.RWMutex` or `sync.Map`
- Slice append from multiple goroutines (len/cap not thread-safe)

```go
// BAD
var counter int
go func() { counter++ }()

// GOOD
var counter atomic.Int64
go func() { counter.Add(1) }()
```

## Channel patterns

Wrong direction — always specify channel direction in function signatures:
```go
// BAD
func producer(ch chan int)

// GOOD
func producer(ch chan<- int)
func consumer(ch <-chan int)
```

Closing a channel from the wrong side — only sender closes:
```go
// BAD — receiver closes
func consumer(ch <-chan int) {
    close(ch)
}

// GOOD — sender closes when done sending
func producer(ch chan<- int) {
    defer close(ch)
    for _, v := range items {
        ch <- v
    }
}
```

## Select

Missing `default` causes block; missing `ctx.Done()` causes leak:
```go
// BAD — blocks forever if nothing ready
select {
case v := <-ch:
    process(v)
}

// GOOD
select {
case v := <-ch:
    process(v)
case <-ctx.Done():
    return ctx.Err()
}
```

## Mutex vs Channel

- Mutex — protecting shared state
- Channel — passing ownership / signaling

```go
// BAD — using channel as mutex
lock := make(chan struct{}, 1)
lock <- struct{}{}
counter++
<-lock

// GOOD
var mu sync.Mutex
mu.Lock()
counter++
mu.Unlock()
```

## WaitGroup misuse

```go
// BAD — Add inside goroutine (race with Wait)
for _, item := range items {
    go func() {
        wg.Add(1)
        defer wg.Done()
        process(item)
    }()
}

// GOOD
for _, item := range items {
    wg.Add(1)
    go func() {
        defer wg.Done()
        process(item)
    }()
}
```
