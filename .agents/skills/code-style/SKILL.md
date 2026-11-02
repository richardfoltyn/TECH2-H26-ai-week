---
name: code-style
description: Fix formatting, lint, comments, and docstrings in user-specified Python files; report notebook structure and presentation issues for the user to decide.
disable-model-invocation: true
---

# Python Code Style

Review and fix only the files or directories specified by the user. For
directories, include Python scripts (`.py`) and Jupyter notebooks (`.ipynb`).

Apply Ruff's configured lint fixes and directly fix formatting, comments, and
docstrings. Do not manually refactor code. Preserve execution order.

Review notebook structure and presentation, but report shortcomings without
fixing them. The user decides whether to make those changes.

## All Python code

### Ruff formatting and lint fixes

- Before the manual review, start by running `ruff format` on the specified
  paths, using the project's existing Python environment and Ruff configuration.
- Next, run `ruff check --fix` on those paths to apply the configured lint fixes.
- Run Ruff through the environment specified in the repository instructions.
  Do not install tools or change the Ruff configuration.

### Spacing and comments

- Separate distinct logical blocks with a single blank line.
- Add missing line comments to explain complex expressions and operations,
  including complicated pandas transformations.
- For nontrivial mathematical expressions, add the corresponding formula in a
  comment above the code.
- Keep comments concise and focused on the purpose of logical steps or
  complicated operations.

### Docstrings

- Use NumPy-style docstrings.
- Add missing docstrings for nontrivial functions and fix existing docstrings.
- Start with a one-line summary, followed by further explanation where useful.
- Describe parameters and return values where useful, ensuring the descriptions
  match the code.
- Use double backticks for inline code.
- Preserve existing factual content and useful details.
- For a single return value, omit its variable name from the Returns section.
  For multiple return values, describe each separately.
- Give scripts a concise module-level docstring explaining their purpose.

## Jupyter notebooks

Apply the Python formatting, lint, comment, and docstring fixes above directly
to notebook code cells. Remove trailing blank lines from edited cells. Preserve
the number and order of cells, existing Markdown, and mathematical notation.

For the following organization and presentation criteria, identify and report
all shortcomings. Do not split, merge, add, remove, or reorder cells, rewrite
explanatory Markdown, or change plotting and output code to address them.

### Organization to review

- Markdown headings clearly distinguish sections and subsections.
- Concise Markdown explanations introduce major analysis steps.
- Code cells are focused on a single purpose.
- Data loading, preparation, computation, and plotting occupy distinct cells.
- Each top-level function is defined in its own code cell.
- Each figure has its own plotting cell.

### Presentation to review

- Explanatory Markdown is concise and visually organized.
- Figures have clear labels, units, legends and annotations where needed, and
  consistent presentation.
- Printed output is concise rather than unnecessarily large.
- Results include explanations where interpretation is needed.
- Explanations of the analysis and interpretations of results appear in Markdown
  cells, not as code comments.

## Verification and report

- After the lint fixes and manual edits, run `ruff format` again on the specified
  paths to format any changes.
- Verify the result with `ruff check --no-fix` and `ruff format --check` on those
  paths.
- Review the diff to confirm that manual changes are purely stylistic and any
  other code changes come from Ruff's configured lint fixes.
- Confirm that notebook cell counts, order, and structure are unchanged.
- Produce a report with separate sections for applied fixes, checks performed,
  and recommendations requiring the user's decision.
- For every recommendation, identify the file and notebook cell or section,
  describe the shortcoming, and suggest a concrete improvement. Leave these
  recommendations unapplied.
- Include unresolved lint findings in the report.
