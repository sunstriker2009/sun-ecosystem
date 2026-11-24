# SUN Product Ideas

This page records early product ideas for the SUN ecosystem.

## CodeFolio by Sun

**Phase 1 complete.** SUN-P002 is a live cross-language reference for Regex, Date & Time, Encoding & Escaping, XPath, and CSV. CodeFolio and Workbench are part of SUN’s productivity family. [Open CodeFolio](https://sunstriker2009.github.io/sun-codefolio/) · [CodeFolio roadmap](https://github.com/sunstriker2009/sun-codefolio/blob/main/docs/ROADMAP.md) · [Workbench](https://github.com/sunstriker2009/sun-workbench)

### Original snippet-builder concept

The early concept adapted SnippetBook’s searchable snippets and editable builders to the web. That workspace now lives in [Playground by Sun](https://sunstriker2009.github.io/sun-playground/). The notes below record the original design.

### Search and reference

- Support plain-language task searches and exact syntax searches. Index snippet titles, aliases, use cases, code and examples, with filters by language or tool.
- Give each snippet a shareable page with a short explanation, realistic examples, expected output or behavior, prerequisites, relevant side effects and related snippets.

### Interactive builder

- Let each snippet define its editable parameters, including their types, defaults and allowed values where applicable.
- Update the code preview as values change and handle quoting or escaping for the target language or command where applicable.
- **Generate and copy.** Set the values and copy the resulting snippet immediately.
- **Save a named variant.** Save the parameter values for a snippet under a name, then reopen, edit and copy the variant on a later visit.

For example, a Git history snippet could let the user choose a branch, set the number of commits and toggle file-change details. The same snippet could have named variants for “Release review” and “Daily changelog.”

### First-release storage proposal

Store named variants in the current browser for the first release. Cross-device access can be evaluated separately.
