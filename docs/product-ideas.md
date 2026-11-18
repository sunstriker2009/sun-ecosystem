# SUN Product Ideas

This page records early product ideas for the SUN ecosystem.

## CodeBook by Sun

**Status:** Product idea  
**Working name:** CodeBook by Sun  
**Alternate name:** SnippetBook by Sun, if continuity with the Visual Studio extension is the priority.

CodeBook brings the SnippetBook Visual Studio extension concept to an interactive website. It is a quick reference for useful snippets across languages and tools such as Git, JavaScript, C# and XPath. Developers can find a snippet by describing their task, learn from worked examples and tailor the code to their own use.

### Search and reference

- Support plain-language task searches and exact syntax searches. Index snippet titles, aliases, use cases, code and examples, with filters by language or tool.
- Give each snippet a shareable page with a short explanation, realistic examples, expected output or behavior, prerequisites, relevant side effects and related snippets.

### Interactive builder

- Let each snippet define its editable parameters, including their types, defaults and allowed values where applicable.
- Update the code preview as values change and handle quoting or escaping for the target language or command where applicable.
- **Generate and copy.** Set the values and copy the resulting snippet immediately.
- **Save a named variant.** Save the parameter values for a snippet under a name, then reopen, edit and copy the variant on a later visit.

For example, a Git history snippet could let the user choose a branch, set the number of commits and toggle file-change details. The same snippet could have named variants for “Release review” and “Daily changelog.”

### Open question

Where should named variants be stored, and should they follow the user across devices?
