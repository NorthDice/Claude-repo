# Performance

## Slice & Map pre-allocation

When size is known — always pre-allocate:
```go
// BAD — grows with every append (multiple allocations)
var result []int
for _, v := range items {
    result = append(result, v*2)
}

// GOOD
result := make([]int, 0, len(items))
for _, v := range items {
    result = append(result, v*2)
}

// BAD — map grows dynamically
m := make(map[string]int)

// GOOD
m := make(map[string]int, expectedSize)
```

## String concatenation in loops

```go
// BAD — O(n²), new allocation every iteration
result := ""
for _, s := range items {
    result += s
}

// GOOD
var sb strings.Builder
sb.Grow(totalLen) // optional: pre-allocate if known
for _, s := range items {
    sb.WriteString(s)
}
result := sb.String()
```

## Unnecessary allocations

```go
// BAD — []byte allocation for every comparison
if string(b) == "hello" { ... }

// GOOD
if bytes.Equal(b, []byte("hello")) { ... }

// BAD — sprintf for simple concat
s := fmt.Sprintf("%s/%s", a, b)

// GOOD
s := a + "/" + b
```

## sync.Pool

Use for frequently allocated short-lived objects (buffers, decoders):
```go
var bufPool = sync.Pool{
    New: func() any { return new(bytes.Buffer) },
}

buf := bufPool.Get().(*bytes.Buffer)
buf.Reset() // always reset before use
defer bufPool.Put(buf)
```

## Struct field alignment

Order fields from largest to smallest to reduce padding:
```go
// BAD — wastes 7 bytes of padding
type Bad struct {
    a bool    // 1 byte + 7 padding
    b float64 // 8 bytes
    c bool    // 1 byte + 7 padding
} // total: 24 bytes

// GOOD
type Good struct {
    b float64 // 8 bytes
    a bool    // 1 byte
    c bool    // 1 byte + 6 padding
} // total: 16 bytes
```

## Escape analysis

Returning pointer to local variable causes heap allocation:
```go
// Causes heap allocation — only do if lifetime exceeds function
func newUser() *User {
    return &User{} // escapes to heap
}

// If used only within function — prefer value
func process() {
    u := User{} // stays on stack
    u.validate()
}
```
