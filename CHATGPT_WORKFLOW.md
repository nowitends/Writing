# ChatGPT workflow for `dchorazkiewicz/Lectures_notes_old_school`

This file is the single working instruction for ChatGPT when assisting with this repository.

## 1. Select the correct repository in the ChatGPT app

Before doing any GitHub work, the correct repository must be selected in the ChatGPT app UI.

In the message box:

1. Click the `GitHub` connector selector.
2. Choose:

```text
dchorazkiewicz/Lectures_notes_old_school
```

3. Make sure the active connector namespace is:

```text
GitHub/dchorazkiewicz/Lectures_notes_old_school
```

Do not continue with reads or writes if the active namespace is:

```text
GitHub/dchorazkiewicz/Mathematics_Physics_Lectures
```

or any other repository.

Selecting repository access in the GitHub App settings is not enough. The active repository must also be selected inside the ChatGPT app through the GitHub selector.

## 2. Default repository and branch

Use this repository by default:

```text
dchorazkiewicz/Lectures_notes_old_school
```

Use this branch by default:

```text
main
```

Do not use another repository or another branch unless the user explicitly says so.

## 3. GitHub App configuration

The ChatGPT Codex Connector / GitHub App should be installed for the GitHub account:

```text
dchorazkiewicz
```

The repository access setting should be:

```text
All repositories
```

The connector must have:

```text
Read and write access to code
```

This is required for creating, updating, deleting, and committing files.

If writes fail with:

```text
403 Resource not accessible by integration
```

then check both:

1. GitHub App permissions, especially code / contents write access.
2. The active repository selected in the ChatGPT app GitHub selector.

## 4. Reading files: always use full GitHub URLs

For reading files, use full GitHub URLs with the `fetch` action.

The base URL is:

```text
https://github.com/dchorazkiewicz/Lectures_notes_old_school/blob/main/
```

If the user gives a path relative to the repository root, append it to the base URL.

Example user path:

```text
Phys/chapters/kinematics/velocity.tex
```

Full URL to read:

```text
https://github.com/dchorazkiewicz/Lectures_notes_old_school/blob/main/Phys/chapters/kinematics/velocity.tex
```

Use:

```text
GitHub/dchorazkiewicz/Lectures_notes_old_school.fetch
```

with the full URL.

Do not use short paths for ordinary reading. Do not read from another repository unless explicitly instructed.

## 5. Repository tree

Before tasks that depend on locating files, resolving relative paths, understanding the project structure, or editing files, first read:

```text
https://github.com/dchorazkiewicz/Lectures_notes_old_school/blob/main/tree.txt
```

The repository currently has:

```text
tree.txt
```

There is no `tree.md` unless it is added later. If the user explicitly points to a later `tree.md`, use that file only after verifying it by full URL.

## 6. Path resolution

The user often gives paths relative to the repository root.

Treat:

```text
Phys/chapters/kinematics/velocity.tex
```

as:

```text
https://github.com/dchorazkiewicz/Lectures_notes_old_school/blob/main/Phys/chapters/kinematics/velocity.tex
```

For write operations, use the relative path only because GitHub write actions require a repository path:

```text
repository_full_name: dchorazkiewicz/Lectures_notes_old_school
path: Phys/chapters/kinematics/velocity.tex
branch: main
```

For read operations, use the full URL.

## 7. Standard procedure before editing

Before editing any file:

1. Confirm that the active connector namespace is `GitHub/dchorazkiewicz/Lectures_notes_old_school`.
2. Read `tree.txt` using the full URL:

```text
https://github.com/dchorazkiewicz/Lectures_notes_old_school/blob/main/tree.txt
```

3. Resolve the target file path from the repository root.
4. Read the target file using its full GitHub URL.
5. Modify only the requested file and requested section.
6. Commit to `main` unless the user explicitly asks for another branch.
7. Verify the result by reading the changed file again using its full GitHub URL.

## 8. Write operations

For writes, use the active namespace:

```text
GitHub/dchorazkiewicz/Lectures_notes_old_school
```

and the repository:

```text
dchorazkiewicz/Lectures_notes_old_school
```

Do not write if the namespace belongs to another repository.

## 9. Write-access test

A minimal write test may create a small file such as:

```text
tmp_write_check_correct_repo.md
```

in:

```text
dchorazkiewicz/Lectures_notes_old_school
```

After such a test, remove the temporary file if deletion is available. If deletion is blocked by the tool safety layer, report that explicitly.

## 10. Important failure mode

If a commit appears in:

```text
dchorazkiewicz/Mathematics_Physics_Lectures
```

then the wrong repository was selected in the ChatGPT app connector selector.

The fix is not only changing GitHub App permissions. The user must select:

```text
dchorazkiewicz/Lectures_notes_old_school
```

inside the ChatGPT GitHub selector in the message box.
