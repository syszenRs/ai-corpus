---
description: Initialize the documentation in a given repository
---

Initialize the documentation for a given repository

### Step 1

If any `./docs` already exists, STOP and say `CANNOT PROCEED - DOCS ALREADY STARTED`

### Step 2

First, invoke the skill `skill({ name: 'index-knowledge' })` with

<user-request>
Analyze this repository to understand its purpose, structure, and behavior.  
No documentation exists yet.  
Generate clear, accurate documentation that explains what the project.  
Create Document only about what is present in the repository and avoid assumptions.
</user-request>
