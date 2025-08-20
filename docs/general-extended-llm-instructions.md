# GitHub Copilot Project Guidelines

## 1. Language Rules
- All **code generation and documentation** must be in **English**.
- **UI content, placeholder text, example data, or mock content** may be in other languages only if explicitly requested.

---

## 2. Coding Style Compliance
- Always include a **Markdown file in `docs/`** defining the **project’s coding style guide**.
- This style guide must be followed for formatting, naming, structure, etc.
- If it's missing or unclear, **ask for clarification before generating any code**.

---

## 3. Documentation Requirements
- All project documentation must reside in `docs/` as Markdown files.
- All **functionalities**, **endpoints**, and **workflows** must be fully documented.
- If code generation **adds or modifies**:
  - DTOs
  - Types / Interfaces
  - Functionality  
  → You must update the corresponding documentation Markdown files.

- **README.md** must include:
  - Project description
  - High-level functionality overview
  - Usage instructions
  - Installation steps  
  Detailed information should be linked to Markdown docs in `docs/`.

---

## 4. Code Quality Standards
- Enforce:
  - **SOLID Principles**
  - **DRY Principle**
  - **Vertical Slice Clean Architecture** with **Ports & Adapters**
- Prioritize readability, maintainability, and scalability.
- Use clear, meaningful naming for functions, variables, classes.

---

## 5. Testing — Test-First Discipline
- **Every method or function must have an associated unit test**.
- Always follow a **Test-First** (TDD) approach: **write the unit test before writing the implementation**.
- For each testing technology or framework, **search for and apply the most appropriate approach** first (e.g., JUnit, pytest, xUnit).
- Tests must be:
  - Self-contained
  - Following the Arrange-Act-Assert pattern (or project convention)
  - Cover both happy paths and edge cases  
  These practices align with TDD and improve code reliability and design :contentReference[oaicite:0]{index=0}.

---

## 6. Diagramming Standard
- **Every diagram in any Markdown file** (especially in `docs/`) must be authored using **embedded PlantUML or Mermaid syntax**.
  - Use fenced code blocks with `plantuml` or `mermaid` tags.
  - Do **not** use external images or proprietary formats.

---

## 7. Architectural Guidelines
- Use **Vertical Slice Clean Architecture** with Ports & Adapters.
- Maintain clear separation into:
  - **Domain Layer**: Entities, business logic
  - **Application Layer**: Use cases, orchestration
  - **Infrastructure Layer**: Adapters for frameworks, storage, external systems
- Apply **Dependency Inversion** to keep domain logic decoupled.

---

## 8. Interaction with Copilot
When generating or modifying code:
1. Locate and apply the coding style guide from `docs/`; ask if it’s missing.
2. Follow **Test-First**: write the unit test first, using the appropriate framework.
3. Update relevant documentation and include diagrams (if needed) using PlantUML or Mermaid.
4. Respect Clean Architecture and Vertical Slice boundaries.
5. Deliver **commit-ready code** without placeholder stubs unless explicitly requested.

---

## 9. Commit & Review Standards
- Commit messages must be **clear, concise**, and explanatory.
- Group logically connected changes into coherent commits.
- Reference related tickets/issues when relevant.
- **Peer review is required** before merging into main branches.
