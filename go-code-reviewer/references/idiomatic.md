# Idiomatic Go

## Naming

- Acronyms all-caps: `HTTPServer`, `userID`, `parseURL` — not `HttpServer`, `userId`
- No `Get` prefix on getters: `user.Name()` not `user.GetName()`
- Error variables: `ErrSomething` / error types: `SomethingError`
- Single-method interfaces end in `-er`: `Reader`, `Closer`, `Stringer`
- Short receiver names: `u` for `User`, `s` for `Server` — consistent across all methods

## Receivers

- Consistent receiver type per type — don't mix pointer and value receivers
- Use pointer receiver if: method mutates state, struct is large, needs to satisfy interface with pointer methods
- Value receiver for small read-only structs

```go
// BAD — mixed receivers on same type
func (u User) Name() string { return u.name }
func (u *User) SetName(n string) { u.name = n }

// GOOD — all pointer if any method needs mutation
func (u *User) Name() string { return u.name }
func (u *User) SetName(n string) { u.name = n }
```

## Interfaces

- Define at the point of use (consumer), not at the point of implementation
- Small interfaces — prefer composing `io.Reader` + `io.Closer` over one big interface
- Accept interfaces, return structs

```go
// BAD — defined next to implementation
package storage
type Storage interface { ... }
type PostgresStorage struct{}
func (p *PostgresStorage) implement Storage

// GOOD — defined where consumed
package service
type Repository interface {
    FindUser(ctx context.Context, id int) (*User, error)
}
```

## Context

- Always first argument: `func Do(ctx context.Context, ...)`
- Never store in struct (except request-scoped objects with clear lifecycle)
- Propagate from caller — don't create `context.Background()` inside handlers

```go
// BAD
func (s *Server) Handle(req *Request) {
    ctx := context.Background() // ignores caller's deadline
    s.db.Query(ctx, ...)
}

// GOOD
func (s *Server) Handle(ctx context.Context, req *Request) {
    s.db.Query(ctx, ...)
}
```

## Struct design

- Don't export fields that don't need to be — use constructor + methods
- Use embedding for behaviour composition, not hierarchy
- Zero value should be useful when possible

```go
// BAD — all fields exported, no encapsulation
type User struct {
    Name string
    Age  int
}

// GOOD
type User struct {
    name string
    age  int
}
func NewUser(name string, age int) *User { ... }
func (u *User) Name() string { return u.name }
```

## Go Proverbs (check against these)

- "Don't communicate by sharing memory, share memory by communicating"
- "The bigger the interface, the weaker the abstraction"
- "Make the zero value useful"
- "A little copying is better than a little dependency"
- "Clear is better than clever"
- "Errors are values"
