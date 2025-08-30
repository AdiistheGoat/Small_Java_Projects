# Differentiation Calculator (Java)

A simple symbolic differentiation tool that parses a math expression (e.g., `3x^3 + 2sin(x)`) and returns its derivative in symbolic form. The program tokenizes the input, builds an expression tree, applies differentiation rules, and simplifies the result.

---

## Libraries Used
- **Java SE (standard library only):** parsing, data structures, I/O

---

## Methodology

**1) Tokenization**  
The input string is first split into meaningful tokens — numbers, variables (`x`), operators (`+ - * / ^`), functions (`sin cos tan ln exp`), and parentheses. This removes spacing ambiguity and prepares the expression for parsing.

**2) Parsing (AST construction)**  
Tokens are converted into an **Abstract Syntax Tree (AST)** using standard operator-precedence parsing (handling precedence/associativity for `^`, `* /`, `+ -`, and parentheses).  
- Leaves: constants and variables  
- Internal nodes: unary functions (e.g., `sin(·)`, `ln(·)`) and binary operators (e.g., `+`, `*`, `^`)

**3) Symbolic Differentiation**  
The AST is traversed recursively to apply standard differentiation rules:
- **Constants/Variable**: `d/dx(c)=0`, `d/dx(x)=1`  
- **Sum/Difference**: `(f ± g)' = f' ± g'`  
- **Product**: `(fg)' = f'g + fg'`  
- **Quotient**: `(f/g)' = (f'g - fg')/g^2`  
- **Power**:  
  - `d/dx(x^n) = n·x^(n-1)` for constant `n`  
  - General form via `f^g = exp(g·ln f)` when needed  
- **Chain Rule**: `(h(u(x)))' = h'(u(x)) · u'(x)`  
- **Common functions**:  
  - `(sin u)' = cos u · u'`  
  - `(cos u)' = -sin u · u'`  
  - `(tan u)' = sec^2 u · u'`  
  - `(ln u)' = (1/u) · u'`  
  - `(exp u)' = exp(u) · u'`

**4) Simplification**  
After differentiation, the tree is simplified to a readable closed form:
- Combine constants, eliminate zero/one factors (`0·f → 0`, `1·f → f`)  
- Flatten nested sums/products  
- Basic algebraic cleanup (e.g., `(a·x^1) → a·x`, `(x^0) → 1` when valid)

**5) Pretty Printing**  
The simplified AST is rendered back to a string with minimal parentheses while preserving operator precedence (e.g., `(3x^2 + 2cos(x))`).

---

## Supported Input (typical)
- **Numbers & variable**: `3`, `-7`, `x`  
- **Operators**: `+  -  *  /  ^`  
- **Functions**: `sin(·)`, `cos(·)`, `tan(·)`, `ln(·)`, `exp(·)`  
- **Parentheses** for grouping

**Examples**
- Input: `3x^3 + 2sin(x)` → Output: `9x^2 + 2cos(x)`  
- Input: `(x^2 + 1)/(x - 1)` → Output: `((2x)(x - 1) - (x^2 + 1))/((x - 1)^2)`  
- Input: `exp(2x)` → Output: `2·exp(2x)`  
- Input: `ln(x^2 + 1)` → Output: `(2x)/(x^2 + 1)`

---

## Notes / Limitations
- Assumes **`x`** is the differentiation variable.  
- Whitespaces are ignored; malformed expressions may produce parse errors.  
- Power rule for **general `f(x)^g(x)`** falls back to `exp(g·ln f)` (requires `f>0` in strict math terms).  
- Simplification is **basic** (not a CAS). Extremely complex expressions may print with extra parentheses.

---
