# Style and Documentation Guidelines

The purpose of this document is to establish Project Aeon code style and documentation guidelines.

We generally adhere to [pep8](https://www.python.org/dev/peps/pep-0008/), [pep257](https://www.python.org/dev/peps/pep-0257/), and [numpy's style guide](https://numpydoc.readthedocs.io/en/latest/format.html) for code style and docstring style guidelines, for all programming languages we use. We run black and flake8 to format our Python code, the config settings for which can be found in our `pyproject.toml` and `.flake8` files.

## General Guidelines

* All files contain a header that briefly describes the contents within a few sentences.
* Code blocks/sections are enclosed in comments that begin and end with `<s` and `/s>`, respectively. Nested subsections are used by adding an `s` for each nesting; e.g., a subsubsection begins and ends with `<sss` and `/sss>`, respectively.
* In general, more lines for the sake of clarity is preferred over brevity.

## Function and Class Docstrings

* Function names should describe the action they perform. Functions have the following sections in the given order:
	- One-line summary description, typically as a verb phrase
	- Long description (optional)
	- Inputs
	- Outputs
	- Examples (optional if included in a separate file)
	- Warnings/Exceptions (optional)
	- Additional notes (optional)
	- See also (optional)
	- Todos (optional)
* Class names should describe the entity they represent. Classes have the following sections in the given order:
	- One-line summary description, typically as a noun phrase
	- Long description (optional)
	- Examples (optional if included in a separate file)
	- Warnings/Exceptions (optional)
	- Additional notes (optional)
	- See also (optional)
	- Todos (optional)

## Whitespace conventions

* A tab/indent is set at four spaces.
* Vertical whitespace is used sparingly, but can be used to improve readability between code blocks/sections.
* Horizontal whitespace is used sparingly, but can be used to improve readability between long and/or complex operations and conditionals.
* Each line contains no more than 79 characters. Whitespace is used to align statements that span multiple lines via a hanging indent or single indent.
* Docstrings are followed by a blank line before the code begins.
* Line terminations are LF, not CRLF.

## Comment conventions

* Block comments are written as full sentences above the corresponding code. 
* Inline comments are written as a short phrase that starts two spaces after the corresponding code.
* Code referenced in comments are surrounded by back ticks for readability.
* Comments are used to describe variables where they are declared.

## Additional Conventions

* Naming conventions:
	- Variable and function names are in lower snake_case (e.g. `exp_ref`, `infer_parameters` with a `_` in between each individual word representation).
	- Classes are in upper Snake_Case (e.g. `Alyx_Panel`).
	- Prefix 'n' is used for integer values e.g. `n_items`.
	- Suffix 'num' is used for referring to a particular instance e.g. `item_num`.
	- Suffices that indicate unit measurement are used when using multiple units e.g. `wheel_deg` and `wheel_mm`.
	- Re-use of variable names (i.e. mutation) is avoided.
	- Same variable names across files have the same meanings.
* Comments are for explaining _what_ a particular chunk of code does when it may be unintuitive, not for explaining exactly _how_ the code does what it does.
* Block comments read as a narrative.
* Complex conditional expressions are avoided; they are replaced with logical variables.
* Imports are organized just below a file's header, in three sections: 1) packages belonging to the standard library, 2) popular packages, 3) personal packages.
* In function calls, parameters should be specified.
* Leading underscores are reserved for "private" functions.
