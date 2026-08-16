# README Structures

Decision guide for choosing and ordering README sections based on project type.

## Audience identification

Before selecting a structure, identify the primary reader:

- End user
- Developer integrating the project
- Contributor
- Operator or deployment engineer

Prioritize sections based on the primary reader.

## Common structures

### Library or SDK

1. Project name and one-line description
2. Installation
3. Quickstart / minimal example
4. API overview or main concepts
5. Configuration
6. Examples
7. Contributing or development setup
8. License

### CLI or tool

1. Project name and one-line description
2. Installation
3. Usage and flags
4. Configuration
5. Examples
6. Troubleshooting
7. License

### Service or API

1. Project name and one-line description
2. What it does
3. Quickstart
4. Endpoints or features
5. Authentication or access
6. Examples
7. Deployment or hosting
8. License

### Template or starter

1. Project name and what it includes
2. Prerequisites
3. Setup
4. Customization guide
5. Examples of what was produced
6. License

## Section rules

- Front-load the value proposition and the fastest path to a working example.
- Do not bury installation or usage under marketing sections.
- If a section is empty or placeholder, remove it instead of leaving TODO text.
- If the project has a logo or icon that is clearly intended for the README header, use it once near the title.
- Do not add "Contributing", "Changelog", or "License" sections when those topics are covered by dedicated files.

## Dependency documentation

Only document dependencies users need to know about. Do not list every internal dependency.
