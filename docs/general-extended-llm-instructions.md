# GitHub Copilot Project Guidelines

## 1. Language Rules
- All **code generation and documentation** must always be in **English**.
- **UI content, placeholder text, example data, or mock content** may be in other languages **only if explicitly requested**.

---

## 2. Coding Style Compliance
- There will always be a **Markdown file** in the `docs` directory containing the **project’s coding style guide**.
- You **must follow the style guide** for:
  - Code structure and formatting.
  - File naming and organization.
  - Documentation format.
- If the style guide is missing or unclear, **ask for it before generating any code**.

---

## 3. Documentation Requirements
- **All documentation must be placed in the `docs` folder** as Markdown files.
- All **functionalities**, **endpoints**, and **workflows** must be **fully documented**.
- If code generation **modifies or adds**:
  - DTOs (Data Transfer Objects)
  - Types / Interfaces
  - Functionality  
  → **Update the relevant documentation Markdown files** in `docs`.

- **README.md** must contain:
  - Project description.
  - Overall functionalities.
  - Usage instructions.
  - Installation procedures.  
  **Detailed information** must be referenced as **links to the relevant Markdown documents** in `docs`.

---

## 4. Code Quality Standards
- Always adhere to:
  - **SOLID Principles**
  - **DRY Principle** – Avoid code duplication.
  - **Clean Architecture (Vertical Slice)** with **Ports & Adapters**.
- Prioritize **readability, maintainability, and scalability**.
- Code must use **meaningful names** for variables, functions, and classes.

---

## 5. Testing Requirements
- For every **new or modified function/method**, create or update **unit tests**.
- Unit tests must:
  - Be self-contained (no external state unless required).
  - Follow **Arrange-Act-Assert** or the project’s established pattern.
  - Cover **happy paths** and **edge cases**.

---

## 6. Architectural Guidelines
- **Default architecture**:  
  - **Vertical Slice Clean Architecture** with Ports & Adapters.
  - Layers:
    - **Domain Layer** – Entities, use cases, business logic.
    - **Application Layer** – Orchestration, service contracts.
    - **Infrastructure Layer** – Frameworks, databases, APIs, adapters.
- Always use **Dependency Inversion** to decouple business logic from external systems.

---

## 7. Interaction with Copilot
When generating or modifying code:
1. **Locate and apply** the project’s coding style guide from `docs`.
2. Update **related documentation** in `docs`.
3. Always generate or update **unit tests**.
4. Use **Clean Architecture principles** and **Vertical Slice boundaries**.
5. Provide **commit-ready code** without incomplete placeholders (unless requested).

---

## 8. Commit & Review Standards
- Commit messages must be **clear and concise**, explaining the change.
- Group logically related changes together.
- Reference related tickets/issues when applicable.
- **Peer review** is required for merges into main branches.
