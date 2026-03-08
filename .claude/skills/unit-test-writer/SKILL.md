---
name: unit-test-writer
description: Write comprehensive unit tests for a function or set of functions. Analyzes inputs, outputs, edge cases, and error conditions. Optimized for Go (table-driven tests) but works for any language.
---

# Unit Test Writer

Generate comprehensive unit tests for the target function(s). Cover all meaningful cases without over-engineering.

## Process

1. **Read the target function(s)** — understand inputs, outputs, return types, and error paths
2. **Identify test cases:**
   - Happy path (normal, expected inputs)
   - Edge cases (empty, nil, zero, boundary values)
   - Error/failure cases (invalid input, expected errors/panics)
   - Boundary values (min, max, off-by-one)
3. **Write the tests** using the project's existing test style

## Go: Table-Driven Tests (default)

```go
func TestFunctionName(t *testing.T) {
    tests := []struct {
        name    string
        input   InputType
        want    OutputType
        wantErr bool
    }{
        {
            name:  "happy path",
            input: validInput,
            want:  expectedOutput,
        },
        {
            name:    "returns error on nil input",
            input:   nil,
            wantErr: true,
        },
        {
            name:  "empty string",
            input: "",
            want:  defaultOutput,
        },
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := FunctionName(tt.input)
            if (err != nil) != tt.wantErr {
                t.Errorf("FunctionName() error = %v, wantErr %v", err, tt.wantErr)
                return
            }
            if got != tt.want {
                t.Errorf("FunctionName() = %v, want %v", got, tt.want)
            }
        })
    }
}
```

## Rules

- Use `testify/assert` if it's already imported in the project; otherwise use standard `testing`
- Match the package name of the file under test (use `_test` suffix package for black-box tests)
- One `Test*` function per function under test
- Name test cases descriptively: `"returns error when input is empty"` not `"test1"`
- Do NOT test unexported internals unless the file already does so
- Do NOT add mocks/fakes unless the function has external dependencies (DB, HTTP, etc.)
- Keep tests in the same directory as the file under test

## Steps to execute

1. Ask the user which function(s) to test if not specified, or read the provided file/function
2. Read the source file to understand the function signature and logic
3. Check if a `*_test.go` file already exists — if so, append to it rather than creating a new one
4. Check for existing test helpers or `testify` usage in the package
5. Write the tests
6. Run `go test ./...` (or the relevant path) to verify they pass
