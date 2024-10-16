# emacs-lisp-doc

-------------------------------------------------
## Emacs Lisp Syntax
-------------------------------------------------
*Emacs Lisp* is a dialect of "Lisp" widely used for extending and customizing the *Emacs* editor. It features typical characteristics of the Lisp language, such as symbol manipulation, recursion, list operations, etc. Below is an overview of Emacs Lisp syntax, covering commonly used basic concepts and features.

## 1. Expressions

In Emacs Lisp, code consists of expressions, which are usually lists enclosed in parentheses. The first element of the list is an operator or function, followed by its arguments.

```lisp
(+ 2 3)  ;; Addition operation, returns 5

```

## 2. Symbols

Symbols are one of the basic data types in *Lisp*, used to represent variables, function names, constants, etc.

```lisp
(setq my-var 42)  ;; Define variable my-var and assign it the value 42
my-var            ;; Refer to variable my-var, returns 42

```

## 3. Function Definition

Use `defun` keyword to define a function.

```lisp
(defun square (x)
  "Return the square of X."
  (* x x))

(square 4)  ;; Returns 16

```

## 4. Conditional Statements

Conditional checks typically use `if` or `cond` statements.

```lisp
(if (> 3 2)
    (message "3 is greater than 2")
  (message "2 is greater than 3"))

;; Using cond for multiple condition checks
(cond
 ((> 3 2) (message "3 is greater than 2"))
 ((< 3 2) (message "3 is less than 2"))
 (t (message "3 is equal to 2")))

```

## 5. Variables

Emacs Lisp supports global and local variables.

Global variables are set using `setq`:

```lisp
(setq my-var 100)  ;; Set global variable my-var to the value 100

```

Local variables are bound using `let`:

```lisp
(let ((a 10)
      (b 20))
  (+ a b))  ;; Returns 30, a and b are local variables

```

## 6. List Operations

Lists are a fundamental data structure in Emacs Lisp, operable using `car` and `cdr`.

```lisp
(setq my-list '(1 2 3 4))

(car my-list)   ;; Returns the first element of the list, result is 1
(cdr my-list)   ;; Returns the rest of the list, result is (2 3 4)
(cons 0 my-list) ;; Returns a new list (0 1 2 3 4)

```

## 7. Loops

Common loop structures include `while` and `dolist`.

```lisp
;; Using while loop
(setq i 0)
(while (< i 5)
  (message "i is %d" i)
  (setq i (1+ i)))

;; Using dolist to loop through a list
(dolist (element '(1 2 3 4 5))
  (message "Element: %d" element))

```

## 8. Function Mapping

Use `mapcar` to apply a function to each element of a list.

```lisp
(mapcar #'square '(1 2 3 4))  ;; Returns (1 4 9 16)

```

## 9. Closures

Emacs Lisp supports closures; you can define and return another function within a function.

```lisp
(defun make-adder (x)
  (lambda (y) (+ x y)))

(setq add-five (make-adder 5))
(funcall add-five 3)  ;; Returns 8

```

## 10. File and Buffer Operations

Emacs Lisp provides a rich API for handling files and buffers.

```lisp
(find-file "~/example.txt")    ;; Open file
(insert "Hello, Emacs Lisp!")  ;; Insert text into the current buffer
(save-buffer)                  ;; Save buffer contents
(kill-buffer)                  ;; Close buffer

```

## 11. Error Handling

Use `condition-case` to catch and handle exceptions.

```
(condition-case nil
    (delete-file "non-existent-file.txt")
  (error (message "An error occurred")))

```

## 12. Macros

Macros are code that generates code. Use `defmacro` to define macros.

```
(defmacro unless (condition &rest body)
  `(if (not ,condition)
       (progn ,@body)))

(unless nil
  (message "This will be printed."))

```

## 13. String Processing

Emacs Lisp provides a rich set of string manipulation functions.

```
(concat "Hello, " "world!")   ;; Concatenate strings, returns "Hello, world!"
(substring "Hello, world!" 0 5) ;; Extract substring, returns "Hello"
(string-match "world" "Hello, world!") ;; Find substring position, returns 7

```

## 14. Key Bindings

Customize key bindings through Emacs Lisp.

```
(global-set-key (kbd "C-c C-c") 'comment-region)  ;; Bind C-c C-c to comment-region command

```

## 15. Mode Hooks

Mode hooks allow you to execute custom code when a specific mode is loaded.

```
(add-hook 'python-mode-hook
          (lambda ()
            (setq tab-width 4)
            (setq python-indent-offset 4)))

```

## 16. Quoting

In Lisp, `'` or `quote` is used to refer to data, preventing the expression from being evaluated.

```
(setq my-list '(1 2 3))  ;; Define a list, not a function call with 1 2 3

```

Using backquote (```) allows you to insert evaluated expressions into quoted data, in combination with `,` and `,@`.

```
(setq a 1)
(setq my-list `(,a 2 3))  ;; Returns (1 2 3)

(setq my-list2 `(1 2 ,@my-list))  ;; Returns (1 2 1 2 3)

```

## 17. Data Types

Emacs Lisp supports multiple data types, including numbers, strings, symbols, lists, vectors, hash tables, booleans, etc.

Numbers: integers and floating-point numbers.

```
(+ 2 3)   ;; Returns 5
(/ 10 3)  ;; Returns 3

```

Strings: character sequences enclosed in double quotes.

```
(concat "Hello" " " "world")  ;; Returns "Hello world"

```

Symbols: identifiers such as variable names, function names.

```
(symbol-name 'foo)  ;; Returns "foo"

```

Vectors: fixed-length sequences similar to arrays.

```
(setq my-vector [1 2 3])
(aref my-vector 0)  ;; Returns 1

```

Hash Tables: collections of key-value pairs.

```
(setq my-hash (make-hash-table :test 'equal))
(puthash "key" "value" my-hash)
(gethash "key" my-hash)  ;; Returns "value"

```

Booleans: `nil` represents false, non-nil represents true.

```
(if nil
    (message "True")
  (message "False"))  ;; Outputs "False"

```

## 18. Functions and Lambda Expressions

Besides defining named functions with `defun`, you can also use anonymous functions (Lambda expressions).

```lisp
(lambda (x) (* x x))  ;; Returns an anonymous function

(funcall (lambda (x) (* x x)) 3)  ;; Returns 9

```

## 19. Macros

Macros are used to generate code, not to compute values directly. Macros are expanded before code execution.

```lisp
(defmacro my-unless (condition &rest body)
  `(if (not ,condition)
       (progn ,@body)))

(my-unless t
  (message "This won't be printed"))

```

## 20. Scope and Closures

Emacs Lisp uses dynamic scope (dynamic scope), but also supports static scope (lexical scope) by setting lexical-binding.

```lisp
(let ((x 10))
  (lambda (y) (+ x y)))

;; If lexical-binding is enabled
(setq lexical-binding t)

```

## 21. File and Buffer Operations

Emacs Lisp has powerful file and buffer operation capabilities.

```lisp
;; Read file contents
(with-temp-buffer
  (insert-file-contents "~/example.txt")
  (buffer-string))  ;; Returns file contents

;; Write to file
(with-temp-file "~/output.txt"
  (insert "Hello, world!"))

```

## 22. Advanced Error Handling

`condition-case` is used to catch and handle exceptions with more granular control.

```lisp
(condition-case err
    (progn
      (delete-file "non-existent-file.txt"))
  (file-error (message "File error: %s" err)))

```

## 23. Custom Commands and Interactive Functions

Use `interactive` declaration to make a function an Emacs command, which can be run via M-x.

```lisp
(defun my-command ()
  "A simple command."
  (interactive)
  (message "This is a custom command"))

;; Bind command to key
(global-set-key (kbd "C-c c") 'my-command)

```

## 24. Object-Oriented Programming

Emacs Lisp supports an object system (EIEIO), allowing the creation of classes and objects.

```lisp
(defclass my-class ()
  ((slot1 :initarg :slot1 :initform nil)
   (slot2 :initarg :slot2 :initform nil)))

(setq obj (make-instance 'my-class :slot1 1 :slot2 2))
(slot-value obj 'slot1)  ;; Returns 1

```

## 25. Input and Output

Emacs Lisp provides various ways to interact with users:

Messages:

```lisp
    (message "Hello, %s!" "Nick")

```

Prompt user for input:

```lisp
    (read-string "Enter your name: ")

```

Select a file:

```lisp
          (read-file-name "Choose a file: ")

```

## 26. Loops and Iteration

Besides the basic `while` loop, you can also use `dotimes` and `dolist` to iterate over collections.

```lisp
            (dotimes (i 5)
              (message "Iteration %d" i))

            (dolist (item '(1 2 3 4 5))
              (message "Item: %d" item))

```

## 27. Hooks and Advice

Hooks: Hook functions to execute custom code before or after certain operations.
Advice: Add additional behavior before or after a function executes.

```lisp
  (add-hook 'before-save-hook 'my-save-hook)
  Advice: You can add additional behavior before or after a function executes.

```

```lisp
  (defun my-around-advice (orig-fun &rest args)
    (message "Before")
    (apply orig-fun args)
    (message "After"))

  (advice-add 'some-function :around #'my-around-advice)

```

## 28. Custom Minor and Major Modes

You can create custom modes to extend Emacs's functionality.

```lisp
    (define-minor-mode my-minor-mode
      "A simple minor mode."
      :lighter " MyMode"
      :keymap (let ((map (make-sparse-keymap)))
                (define-key map (kbd "C-c m") 'my-command)
                map))

    (define-derived-mode my-major-mode fundamental-mode "MyMode"
      "A simple major mode."
      (setq font-lock-defaults '(nil nil)))

```

## 29. File Operations and Network Requests

Emacs Lisp also supports file operations and network requests:

```lisp
    ;; Download web page content
    (url-retrieve "<https://example.com>"
                  (lambda (status)
                    (switch-to-buffer (current-buffer))))

```

## 30. Debugging and Optimization

Emacs Lisp provides various debugging tools:

`debug` function: Manually trigger debugging.

```lisp
  (debug)

```

E-debug: An advanced debugging tool that allows step-by-step execution of code.

```lisp
(edebug-defun)  ;; Call before function definition to enable edebug

```

