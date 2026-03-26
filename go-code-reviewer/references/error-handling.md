# Error Handling

## Wrapping

Use `%w` to preserve the error chain — `%v` breaks `errors.Is` / `errors.As`:
```go
// BAD — breaks unwrapping
return fmt.Errorf("process: %v", err)

// GOOD
return fmt.Errorf("process: %w", err)
```

## Swallowed errors

```go
// BAD
_ = os.Remove(path)

// BAD — logs but continues as if nothing happened
if err != nil {
    log.Println(err)
}

// GOOD — handle or return
if err != nil {
    return fmt.Errorf("remove %s: %w", path, err)
}
```

## Nil-interface trap

Returning a typed nil as `error` — the interface is not nil:
```go
// BAD — callers checking err != nil will miss this
func do() error {
    var err *MyError // typed nil
    return err       // interface{type: *MyError, value: nil} != nil
}

// GOOD
func do() error {
    return nil
}
```

## Sentinel errors

Define at package level, compare with `errors.Is`:
```go
var ErrNotFound = errors.New("not found")

// BAD
if err == ErrNotFound { ... }

// GOOD
if errors.Is(err, ErrNotFound) { ... }
```

## Error type assertion

```go
// BAD
if e, ok := err.(*MyError); ok { ... }

// GOOD — works through wrapping chain
var myErr *MyError
if errors.As(err, &myErr) { ... }
```

## Error naming

- Variables: `ErrSomething`
- Types: `SomethingError`
- Interface: implement `Error() string`

## Early return pattern

```go
// BAD — arrow anti-pattern
func process() error {
    if err == nil {
        if result != nil {
            // more nesting
        }
    }
    return err
}

// GOOD — guard clauses
func process() error {
    if err != nil {
        return fmt.Errorf("process: %w", err)
    }
    if result == nil {
        return ErrEmpty
    }
    // happy path
}
```
