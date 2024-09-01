#### Created: 2024-08-21
#### Tags: [[Clean Code]] [[Checklists]]
# Clean Code Commit Checklist

## 1. Names

- [ ] Are all names meaningful?
- Variables & Constants:
	- [ ] Objects: Describe the value (e.g., user, database)
	- [ ] Numbers or strings: Describe the value
	- [ ] Booleans: True/false question (e.g., isActive, hasPrivilege)
- Functions / Methods:
	- [ ] Operations: Describe the operation (e.g., getUser(..), response.send(..))
	- [ ] Boolean computations: Answer a true/false question (e.g., isValid(...), purchase.isPaid(...))
- Classes: 
	- [ ] Describe the Object (e.g., User, Product, Customer)

## 2. Structure, Comments & Code Formatting

- [ ] Are comments used sparingly and appropriately?
  - [ ] No unnecessary comments (naming should clarify most things)
  - [ ] No dividers/headers for code blocks
  - [ ] Legal comments only at the top of the file
  - [ ] Comments added for unclear things (e.g., regex)
  - [ ] Warnings added where necessary
  - [ ] TODO notes clearly marked
- [ ] Is the code formatting correct?
  - Vertical:
    - [ ] Code is readable like an essay
    - [ ] Long files with multiple concepts are split
    - [ ] Generally one class per file
    - [ ] Appropriate use of blank lines
    - [ ] Similar operations are not split
  - Horizontal:
    - [ ] Long statements are broken into shorter lines

## 3. Functions

- [ ] Are function calls optimized?
  - [ ] Minimal number of parameters (3 or fewer)
  - [ ] Objects used for 3 or more arguments
  - [ ] No output params (no side effects on input props)
- [ ] Is the function body well-structured?
  - [ ] Functions are small and do one thing
  - [ ] Functions work one level of abstraction below their name
  - [ ] Functions are mostly pure (same output for same input, no side effects)
  - [ ] Side effects, if any, are expected
  - [ ] Functions are testable

## 4. Control Structures & Errors

- [ ] Are control structures optimized?
  - [ ] Positive checks are preferred (e.g., isEmpty vs isNotEmpty)
  - [ ] Early returns / guards are used
- [ ] Is error handling appropriate?
  - [ ] Errors are thrown when necessary
  - [ ] Thrown errors are caught

## 5. Classes & Objects

- [ ] Are classes well-designed?
  - [ ] Classes are small with single responsibility
  - [ ] Law of Demeter is followed (no deep object diving)
  - [ ] Classes are open for extension, closed for modification
- [ ] Is object-oriented principle "Tell, don't ask" followed?

Remember to go through this checklist before committing your code to ensure it adheres to clean code principles.

