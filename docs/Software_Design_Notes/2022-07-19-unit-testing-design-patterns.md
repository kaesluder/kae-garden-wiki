# Unit Testing Design Patterns

## `function(args) -> value`

1. Test "happy path"
2. Out-of-range
3. Missing required arg
4. Boolean arg toggle
5. Useful exceptions

## Log and Move On Exception Handling

1. Check that exception isn't bubbled up.
2. Check log message creation.

## External Interfaces

1. Mock for unit testing context.
2. Test happy path and failure cases from services.
3. Mock test cases where remote program things its sending the right thing, but the input is flawed.
4. **Check client library for "hidden" service calls.**
