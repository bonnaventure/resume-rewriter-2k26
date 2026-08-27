# Skill: Batch Resume Rewriter for Job Scrape Data

## Skill Name

`batch-resume-rewriter`

## Description

This skill directs Qwen Coder to find `resume-2026.md`, read job listings from `job-scrape.json`, and generate a tailored resume for each job listing. Each rewritten resume is saved into the `/rewritten` folder.

The skill processes all jobs found in `job-scrape.json` in a single run, creating one output file per job.

The rewrite must follow the rules and parameters defined in `recruiter-rules.md`.

---

## Launch Prompt

This skill can be launched with prompts such as:

```text
rewrite resumes for all jobs
```

or:

```text
process job-scrape.json
```

or simply:

```text
run batch resume rewriter
```

---

## Required Files

Before rewriting, Qwen Coder must locate and read the following files:

### 1. Source Resume

File name:

```text
resume-2026.md
```

This is the master resume that will be rewritten for each job.

### 2. Recruiter Rules

File name:

```text
recruiter-rules.md
```

This file contains the parameters, constraints, tone, formatting rules, and rewriting instructions that must be followed.

### 3. Job Scrape Data

File name:

```text
job-scrape.json
```

This JSON file contains an array of job listings. Each job listing should include at minimum:
- Company name
- Job title
- Job description text
- Any other relevant metadata (location, posting date, etc.)

Example structure:

```json
[
  {
    "company": "Example Corp",
    "title": "Senior Marketing Manager",
    "description": "Job description text here...",
    "posted_date": "2026-01-15"
  }
]
```

If `job-scrape.json` cannot be found, Qwen Coder should stop and report the error.

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

and:

```text
job-scrape.json
```

If any of these files cannot be found, Qwen Coder should stop and clearly tell the user which required file is missing.

The `job-scrape.json` file may be located in the root directory or in a subfolder. If the user provides a path, use that path.

---

## Output File Naming Convention

Each rewritten resume must be saved into a folder named:

```text
/rewritten
```

If the folder does not exist, Qwen Coder should create it.

The output file name must follow this format:

```text
Jaron-Whittingham-[Company]-[JobTitle]-[Date].md
```

Where:
- `[Company]` is the company name from the job listing (spaces replaced with hyphens, special characters removed)
- `[JobTitle]` is the job title from the job listing (spaces replaced with hyphens, special characters removed)
- `[Date]` is the current date in YYYY-MM-DD format

Example output file names:

```text
Jaron-Whittingham-ExampleCorp-SeniorMarketingManager-2026-01-15.md
Jaron-Whittingham-TechInc-DigitalContentSpecialist-2026-01-15.md
```

If an output file already exists with the same name, Qwen Coder may overwrite it unless the user asks to preserve existing files.

---

## Rewriting Workflow

Qwen Coder must follow these steps in order:

### Step 1: Read Required Files

Read the following files:

```text
resume-2026.md
recruiter-rules.md
job-scrape.json
```

If any file is missing, stop and report the error.

---

### Step 2: Parse Job Listings

Parse the `job-scrape.json` file to extract all job listings.

For each job listing, extract:
- Company name
- Job title
- Job description text
- Any other relevant information (requirements, qualifications, keywords, etc.)

If the JSON structure differs from the expected format, attempt to adapt and extract relevant job information.

---

### Step 3: Process Each Job

For each job listing in `job-scrape.json`, perform the following sub-steps:

#### Sub-step 3a: Analyze the Job Description

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

#### Sub-step 3b: Rewrite the Resume

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

#### Sub-step 3c: Generate Output File Name

Create the output file name using the format:

```text
Jaron-Whittingham-[Company]-[JobTitle]-[Date].md
```

Sanitize the company name and job title by:
- Replacing spaces with hyphens
- Removing special characters except hyphens
- Converting to title case or keeping original casing as appropriate

Use the current date in YYYY-MM-DD format.

#### Sub-step 3d: Save the Output File

Save the rewritten resume to:

```text
/rewritten/Jaron-Whittingham-[Company]-[JobTitle]-[Date].md
```

---

### Step 4: Create the Output Directory

Create the `/rewritten` folder if it does not already exist.

---

## Output Content Structure

Unless `recruiter-rules.md` specifies otherwise, the rewritten resume should be a complete Markdown resume.

A reasonable default structure is:

```md
# Jaron Whittingham

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

Unless forbidden by `recruiter-rules.md`, Qwen Coder may include a hidden Markdown comment at the top of each output file for traceability:

```md
<!-- Rewritten from resume-2026.md for [Company] - [Job Title] using recruiter-rules.md -->
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
Could not find job-scrape.json. Please make sure the file exists in the workspace.
```

```text
job-scrape.json contains no valid job listings. Please check the file format.
```

---

## Completion Response

After successfully writing all rewritten resumes, Qwen Coder should respond with a brief confirmation.

Example:

```text
Batch resume rewrite completed successfully.

Source resume:
resume-2026.md

Rules file:
recruiter-rules.md

Job data file:
job-scrape.json

Jobs processed: 5

Output files:
- /rewritten/Jaron-Whittingham-ExampleCorp-SeniorMarketingManager-2026-01-15.md
- /rewritten/Jaron-Whittingham-TechInc-DigitalContentSpecialist-2026-01-15.md
- /rewritten/Jaron-Whittingham-StartupXYZ-MarketingDirector-2026-01-15.md
- /rewritten/Jaron-Whittingham-BigCo-EcommerceLead-2026-01-15.md
- /rewritten/Jaron-Whittingham-InnovationLabs-ContentStrategy-2026-01-15.md
```

Optionally, Qwen Coder may include a short summary of the main changes made across all resumes.

---

## Rules and Constraints

Qwen Coder must:

1. Never modify `resume-2026.md` unless explicitly instructed to do so.
2. Never modify `recruiter-rules.md`.
3. Never modify `job-scrape.json`.
4. Only create or update output files inside `/rewritten`.
5. Always base the rewritten resumes on `resume-2026.md`.
6. Always apply the instructions in `recruiter-rules.md`.
7. Always tailor each resume to its corresponding job listing from `job-scrape.json`.
8. Always use the correct output naming convention (Jaron-Whittingham-[Company]-[JobTitle]-[Date].md).
9. Always create the `/rewritten` folder if it does not exist.
10. Always stop if a required file is missing.
11. Process all jobs in `job-scrape.json` in a single run.

---

## Examples

### Example 1

User prompt:

```text
rewrite resumes for all jobs
```

Qwen Coder should:

1. Read `job-scrape.json`
2. Read `recruiter-rules.md`
3. Read `resume-2026.md`
4. For each job in `job-scrape.json`:
   - Rewrite the resume according to the recruiter rules and job description
   - Save the result to `/rewritten/Jaron-Whittingham-[Company]-[JobTitle]-[Date].md`

### Example 2

If `job-scrape.json` contains:

```json
[
  {
    "company": "Windmill Technologies",
    "title": "Digital Marketing Lead",
    "description": "We are seeking a Digital Marketing Lead..."
  },
  {
    "company": "Ecommerce Plus",
    "title": "Content Strategy Manager",
    "description": "Join our team as a Content Strategy Manager..."
  }
]
```

Qwen Coder should create:

```text
/rewritten/Jaron-Whittingham-WindmillTechnologies-DigitalMarketingLead-2026-01-15.md
/rewritten/Jaron-Whittingham-EcommercePlus-ContentStrategyManager-2026-01-15.md
```

(assuming the current date is 2026-01-15)

---

## Acceptance Checklist

A successful run must result in:

- [ ] `resume-2026.md` located and read
- [ ] `recruiter-rules.md` located and read
- [ ] `job-scrape.json` located and read
- [ ] All job listings extracted from `job-scrape.json`
- [ ] Resume rewritten for each job according to `recruiter-rules.md`
- [ ] Each resume tailored to its corresponding job description
- [ ] `/rewritten` folder created if missing
- [ ] Output files saved with the correct naming convention (Jaron-Whittingham-[Company]-[JobTitle]-[Date].md)
- [ ] No required source files were modified
- [ ] User receives a confirmation message with all output file paths