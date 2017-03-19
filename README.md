# git-partial-ignores

This is an idea for Git or a tool to support partial file ignores via comments like ESLint.

One use case would be to allow minor changes to configs during development, without
polluting the diff or requiring reverting or partial staging to commit,
and especially to prevent accidental commit.

For example:

```diff
const config = {
-  api: 'https://api.example.com'
+  api: 'http://localhost:9000' // git-ignore
};
```

Or:

```diff
const config = {
-  api: 'https://api.example.com'
+  // git-ignore-next
+  api: 'http://localhost:9000'
};
```

Or:

```diff
const config = {
-  api: 'https://api.example.com',
-  base: 'https://www.example.com'
+  // git-ignore-start
+  api: 'http://localhost:9000',
+  base: 'http://localhost:3000'
+  // git-ignore-end
};
```

## Implementation

Maybe wrap or alias `git` command with custom script. Compatible with github/hub?

E.g. `commit` would do a partial unstage first. Would this be non-trivial to implement? Might have to programmatically modify patches like the `e` mode of `git reset -p`.

Suppress from `diff` by filtering output in a `grep`-like fashion, but supporting blocks.

