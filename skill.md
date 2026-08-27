Below is a ready-to-use `skill.md` you can save for Qwen Coder.

```md
# Skill: Resume Rewriter for Job Descriptions

## Skill Name

`resume-rewriter`

## Description

This skill directs Qwen Coder to find `resume-2026.md`, rewrite it for a specific job description file, and save the rewritten resume into the `/rewritten` folder.

Each job description is a Markdown file ending with `-jobDescription.md`.

Example:

```text
atco-coordinator-jobDescription.md
```

The rewritten resume output file should use the same job description file name and append `-qwen.md`.

Example:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

The rewrite must follow the rules and parameters defined in `recruiter-rules.md`.

---

## Launch Prompt

This skill can be launched with prompts such as:

```text
rewrite for atco-coordinator-jobDescription.md
```

or more generally:

```text
rewrite for <file-name>-jobDescription.md
```

Example:

```text
rewrite for atco-coordinator-jobDescription.md
```

---

## Required Files

Before rewriting, Qwen Coder must locate and read the following files:

### 1. Source Resume

File name:

```text
resume-2026.md
```

This is the master resume that will be rewritten.

### 2. Recruiter Rules

File name:

```text
recruiter-rules.md
```

This file contains the parameters, constraints, tone, formatting rules, and rewriting instructions that must be followed.

### 3. Job Description File

File name pattern:

```text
*-jobDescription.md
```

Example:

```text
atco-coordinator-jobDescription.md
```

This file contains the job description that the resume should be tailored toward.

---

## Input Parsing

When the user runs the skill, Qwen Coder should parse the job description file name from the prompt.

Example user prompt:

```text
rewrite for atco-coordinator-jobDescription.md
```

Qwen Coder should identify:

```text
atco-coordinator-jobDescription.md
```

as the target job description file.

If the user provides only part of the file name, Qwen Coder should attempt to match it to a file ending in `-jobDescription.md`.

Example:

```text
rewrite for atco-coordinator
```

Qwen Coder should look for:

```text
atco-coordinator-jobDescription.md
```

If multiple matching job description files are found, Qwen Coder should list the matches and ask the user to choose one.

If no matching job description file is found, Qwen Coder should report that the file could not be found and list available files ending with `-jobDescription.md`.

---

## File Search Behavior

Qwen Coder should search the workspace for:

```text
resume-2026.md
```

and:

```text
recruiter-rules.md
```

If either file cannot be found, Qwen Coder should stop and clearly tell the user which required file is missing.

Qwen Coder should also search for the requested job description file.

The job description file may be located in the root directory or in a subfolder.

If the user provides a path, use that path.

Example:

```text
rewrite for jobs/atco-coordinator-jobDescription.md
```

Qwen Coder should use:

```text
jobs/atco-coordinator-jobDescription.md
```

as the job description source file.

---

## Output File Rules

The rewritten resume must be saved into a folder named:

```text
/rewritten
```

If the folder does not exist, Qwen Coder should create it.

The output file name must be based on the job description file name.

Take the job description file name and append `-qwen.md`.

Example input job description file:

```text
atco-coordinator-jobDescription.md
```

Example output file:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

If the job description file is located in a subfolder, only use the base file name for the output file.

Example input:

```text
jobs/atco-coordinator-jobDescription.md
```

Example output:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

If an output file already exists with the same name, Qwen Coder may overwrite it unless the user asks to preserve existing files.

---

## Rewriting Workflow

Qwen Coder must follow these steps in order:

### Step 1: Identify the Job Description File

Parse the user prompt to determine which `-jobDescription.md` file is being targeted.

Validate that the file name ends with:

```text
-jobDescription.md
```

If it does not, attempt to append or match the correct file name.

---

### Step 2: Read the Recruiter Rules

Read:

```text
recruiter-rules.md
```

This file defines the rewriting parameters.

Qwen Coder must follow all instructions in `recruiter-rules.md`.

If `recruiter-rules.md` is missing, stop and report the error.

---

### Step 3: Read the Source Resume

Read:

```text
resume-2026.md
```

This is the resume to be rewritten.

If `resume-2026.md` is missing, stop and report the error.

---

### Step 4: Read the Job Description

Read the requested job description file.

Extract relevant information such as:

- Job title
- Company name
- Required qualifications
- Preferred qualifications
- Responsibilities
- Keywords
- Tools and technologies
- Soft skills
- Certifications
- Industry terminology
- Tone or seniority level

Do not fabricate requirements that are not present in the job description.

---

### Step 5: Rewrite the Resume

Rewrite `resume-2026.md` so that it is tailored to the job description.

The rewrite must:

- Follow all rules in `recruiter-rules.md`
- Preserve truthful information from the original resume
- Avoid fabricating jobs, degrees, certifications, employers, dates, or accomplishments
- Improve clarity, relevance, and impact
- Align language with the target job description
- Emphasize transferable skills and relevant experience
- Use keywords from the job description where appropriate
- Maintain a professional tone
- Match the format required by `recruiter-rules.md`

If `recruiter-rules.md` contains formatting instructions, follow those instructions exactly.

If `recruiter-rules.md` contains section order rules, use that section order.

If `recruiter-rules.md` contains length limits, obey those limits.

If `recruiter-rules.md` contains language rules, tone rules, or keyword rules, apply them.

If there is a conflict between the job description and `recruiter-rules.md`, follow `recruiter-rules.md`.

---

### Step 6: Create the Output File

Create the `/rewritten` folder if it does not already exist.

Save the rewritten resume to:

```text
/rewritten/<job-description-file-name>-qwen.md
```

Example:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

---

## Output Content Structure

Unless `recruiter-rules.md` specifies otherwise, the rewritten resume should be a complete Markdown resume.

A reasonable default structure is:

```md
# Candidate Name

## Professional Summary

...

## Core Skills

...

## Professional Experience

...

## Education

...

## Certifications

...

## Additional Information

...
```

However, if `recruiter-rules.md` defines a different structure, Qwen Coder must use the structure defined there.

---

## Optional Header Comment

Unless forbidden by `recruiter-rules.md`, Qwen Coder may include a hidden Markdown comment at the top of the output file for traceability:

```md
<!-- Rewritten from resume-2026.md for atco-coordinator-jobDescription.md using recruiter-rules.md -->
```

Example:

```md
<!-- Rewritten from resume-2026.md for atco-coordinator-jobDescription.md using recruiter-rules.md -->
```

If `recruiter-rules.md` says not to include comments or metadata, do not include this comment.

---

## Error Handling

Qwen Coder should stop and report an error if any required file is missing.

Possible error messages:

```text
Could not find resume-2026.md. Please make sure the file exists in the workspace.
```

```text
Could not find recruiter-rules.md. Please make sure the file exists in the workspace.
```

```text
Could not find the requested job description file: atco-coordinator-jobDescription.md.
```

If no job description file is specified, Qwen Coder should ask the user which job description to use and list available files matching:

```text
*-jobDescription.md
```

Example response:

```text
Please specify which job description file to use. Available files:

- atco-coordinator-jobDescription.md
- city-planner-jobDescription.md
- grants-administrator-jobDescription.md

Run the skill again using:

rewrite for <file-name>-jobDescription.md
```

---

## Completion Response

After successfully writing the rewritten resume, Qwen Coder should respond with a brief confirmation.

Example:

```text
Resume rewritten successfully.

Source resume:
resume-2026.md

Job description:
atco-coordinator-jobDescription.md

Rules file:
recruiter-rules.md

Output file:
/rewritten/atco-coordinator-jobDescription-qwen.md
```

Optionally, Qwen Coder may include a short summary of the main changes made, such as:

- Tailored professional summary
- Reordered sections based on recruiter rules
- Emphasized keywords from the job description
- Adjusted tone or formatting
- Reduced length to match recruiter rules

---

## Rules and Constraints

Qwen Coder must:

1. Never modify `resume-2026.md` unless explicitly instructed to do so.
2. Never modify `recruiter-rules.md`.
3. Never modify the job description file.
4. Only create or update the output file inside `/rewritten`.
5. Always base the rewritten resume on `resume-2026.md`.
6. Always apply the instructions in `recruiter-rules.md`.
7. Always tailor the resume to the selected `-jobDescription.md` file.
8. Always use the correct output naming convention.
9. Always create the `/rewritten` folder if it does not exist.
10. Always stop if a required file is missing.

---

## Examples

### Example 1

User prompt:

```text
rewrite for atco-coordinator-jobDescription.md
```

Qwen Coder should:

1. Find `atco-coordinator-jobDescription.md`
2. Read `recruiter-rules.md`
3. Read `resume-2026.md`
4. Rewrite the resume according to the recruiter rules and job description
5. Save the result to:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

---

### Example 2

User prompt:

```text
rewrite for jobs/atco-coordinator-jobDescription.md
```

Qwen Coder should:

1. Read:

```text
jobs/atco-coordinator-jobDescription.md
```

2. Read:

```text
recruiter-rules.md
```

3. Read:

```text
resume-2026.md
```

4. Save the result to:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

---

### Example 3

User prompt:

```text
rewrite for atco-coordinator
```

Qwen Coder should attempt to match:

```text
atco-coordinator-jobDescription.md
```

If found, it should proceed with the rewrite and save the output to:

```text
/rewritten/atco-coordinator-jobDescription-qwen.md
```

---

## Acceptance Checklist

A successful run must result in:

- [ ] `resume-2026.md` located and read
- [ ] `recruiter-rules.md` located and read
- [ ] Requested `-jobDescription.md` file located and read
- [ ] Resume rewritten according to `recruiter-rules.md`
- [ ] Resume tailored to the target job description
- [ ] `/rewritten` folder created if missing
- [ ] Output file saved with the correct name
- [ ] Output file name ends with `-qwen.md`
- [ ] No required source files were modified
- [ ] User receives a confirmation message with the output file path
```