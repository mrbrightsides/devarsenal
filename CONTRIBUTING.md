# 🤝 Contributing to Dev Arsenal

Thank you for your interest in contributing to **Dev Arsenal**! We're excited to have you join our mission to build next-generation development tools for the community.

This document provides guidelines and instructions for contributing to the project. Whether you're fixing bugs, adding features, improving documentation, or suggesting ideas, your contributions are welcome!

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Getting Started](#-getting-started)
- [Development Workflow](#-development-workflow)
- [How to Contribute](#-how-to-contribute)
- [Contribution Guidelines](#-contribution-guidelines)
- [Pull Request Process](#-pull-request-process)
- [Style Guidelines](#-style-guidelines)
- [Testing](#-testing)
- [Community](#-community)

---

## 📜 Code of Conduct

By participating in this project, you agree to maintain a respectful, inclusive, and collaborative environment. We expect all contributors to:

- Be respectful and considerate of others
- Use welcoming and inclusive language
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards other contributors

Any unacceptable behavior can be reported to [support@elpeef.com](mailto:support@elpeef.com).

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js 18+** (LTS recommended)
- **npm**, **yarn**, or **pnpm** package manager
- **Git** for version control
- **MetaMask** wallet (for testing blockchain features)
- A code editor (VS Code recommended)

### Fork and Clone

1. **Fork the repository** on GitHub by clicking the "Fork" button at the top right.

2. **Clone your fork** to your local machine:
```bash
git clone https://github.com/YOUR_USERNAME/devarsenal.git
cd devarsenal
```

3. **Add upstream remote** to keep your fork synced:
```bash
git remote add upstream https://github.com/mrbrightsides/devarsenal.git
```

### Install Dependencies

```bash
npm install
# or
yarn install
# or
pnpm install
```

### Environment Setup (Optional)

Create a `.env.local` file in the root directory for API keys:

```bash
OPENAI_API_KEY=your_openai_api_key_here
INFURA_PROJECT_ID=your_infura_project_id_here
```

### Run Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Navigate to `http://localhost:3000` to see the app running.

---

## 🔄 Development Workflow

### Sync Your Fork

Before starting work, sync your fork with the upstream repository:

```bash
git checkout main
git fetch upstream
git merge upstream/main
git push origin main
```

### Create a Feature Branch

Always create a new branch for your changes:

```bash
git checkout -b feature/your-feature-name
# or for bug fixes
git checkout -b fix/bug-description
```

Branch naming conventions:
- `feature/` - New features or enhancements
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Adding or updating tests
- `chore/` - Maintenance tasks

### Make Your Changes

1. Write clean, well-documented code
2. Follow the [Style Guidelines](#-style-guidelines)
3. Test your changes thoroughly
4. Commit your changes with clear messages

### Commit Messages

Write clear and descriptive commit messages following this format:

```
type(scope): brief description

Detailed explanation of what changed and why (optional)

Closes #issue_number (if applicable)
```

**Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `style` - Code style/formatting changes
- `refactor` - Code refactoring
- `test` - Adding or updating tests
- `chore` - Maintenance tasks

**Examples:**
```bash
git commit -m "feat(ai-cannon): add support for code explanation mode"
git commit -m "fix(bug-hunter): resolve incorrect line number detection"
git commit -m "docs(readme): update installation instructions"
```

---

## 🎯 How to Contribute

### Types of Contributions

We welcome various types of contributions:

#### 🐛 Bug Reports

Found a bug? Please [open an issue](https://github.com/mrbrightsides/devarsenal/issues/new) with:
- Clear title and description
- Steps to reproduce
- Expected vs. actual behavior
- Screenshots (if applicable)
- Browser/OS information
- Error messages or console logs

#### ✨ Feature Requests

Have an idea? [Open an issue](https://github.com/mrbrightsides/devarsenal/issues/new) with:
- Clear description of the feature
- Use case and benefits
- Proposed implementation (optional)
- Mockups or examples (optional)

#### 📝 Documentation

Help improve our documentation:
- Fix typos or unclear explanations
- Add missing documentation
- Update outdated information
- Create tutorials or guides

#### 💻 Code Contributions

Contribute code improvements:
- Fix bugs
- Implement new features
- Optimize performance
- Refactor code
- Add tests

#### 🎨 Design & UI/UX

Improve the user experience:
- Design new themes
- Enhance UI components
- Improve accessibility
- Create icons or graphics

---

## 📐 Contribution Guidelines

### Code Quality

- **TypeScript**: Use strict typing, avoid `any` where possible
- **Formatting**: Code will be automatically formatted with Prettier
- **Linting**: Ensure no ESLint errors
- **Comments**: Add comments for complex logic
- **DRY Principle**: Don't repeat yourself - extract reusable code
- **Performance**: Consider performance implications of your changes

### Component Structure

When creating new components:

```typescript
// src/components/your-component.tsx
'use client';

import { useState } from 'react';
import { Button } from '@/components/ui/button';

interface YourComponentProps {
  title: string;
  onAction?: () => void;
}

export function YourComponent({ title, onAction }: YourComponentProps) {
  const [state, setState] = useState<boolean>(false);

  return (
    <div className="p-4">
      <h2>{title}</h2>
      <Button onClick={onAction}>Action</Button>
    </div>
  );
}
```

### File Organization

- Place React components in `src/components/`
- Place utility functions in `src/lib/`
- Place API routes in `src/app/api/`
- Place hooks in `src/hooks/`
- Use descriptive, kebab-case file names

### API Routes

When creating API routes, follow this structure:

```typescript
// src/app/api/your-endpoint/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function POST(request: NextRequest) {
  try {
    const body = await request.json();
    
    // Your logic here
    
    return NextResponse.json({ success: true, data: result });
  } catch (error) {
    console.error('API Error:', error);
    return NextResponse.json(
      { success: false, error: 'Internal server error' },
      { status: 500 }
    );
  }
}
```

### Weapon (Feature) Contributions

When adding new "weapons" (features):

1. Create the component in `src/components/`
2. Add weapon metadata to the arsenal system
3. Add appropriate icons and descriptions
4. Update the main navigation
5. Document the feature in README.md
6. Add usage examples

---

## 🔍 Pull Request Process

### Before Submitting

1. ✅ Ensure your code builds successfully (`npm run build`)
2. ✅ Test your changes thoroughly
3. ✅ Update documentation if needed
4. ✅ Add comments to complex code
5. ✅ Follow the style guidelines
6. ✅ Sync with the latest upstream changes

### Submitting a PR

1. **Push your branch** to your fork:
```bash
git push origin feature/your-feature-name
```

2. **Open a Pull Request** on GitHub with:
   - Clear title describing the change
   - Detailed description of what changed and why
   - Link to related issues (e.g., "Closes #123")
   - Screenshots (if applicable)
   - Testing steps

3. **PR Template:**
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Code refactoring

## Related Issues
Closes #

## Testing
How to test these changes

## Screenshots (if applicable)
[Add screenshots here]

## Checklist
- [ ] Code builds successfully
- [ ] Tests pass (if applicable)
- [ ] Documentation updated
- [ ] Follows style guidelines
```

### Review Process

1. Maintainers will review your PR
2. Address any feedback or requested changes
3. Once approved, your PR will be merged
4. Your contribution will be credited in the release notes

### After Your PR is Merged

1. Delete your feature branch (optional but recommended):
```bash
git branch -d feature/your-feature-name
git push origin --delete feature/your-feature-name
```

2. Sync your fork with upstream:
```bash
git checkout main
git pull upstream main
git push origin main
```

---

## 🎨 Style Guidelines

### TypeScript/JavaScript

- Use **TypeScript** for all new code
- Use **strict mode** - explicit types required
- Use **functional components** with hooks
- Use **arrow functions** for event handlers
- Use **async/await** instead of promises
- Use **template literals** for string interpolation

### React Best Practices

- Use **React 19** features and patterns
- Prefer **server components** unless client interactivity is needed
- Use **'use client'** directive when necessary
- Implement proper **error boundaries**
- Handle **loading states** appropriately
- Clean up **side effects** in useEffect

### CSS/Tailwind

- Use **Tailwind CSS** utility classes
- Follow **mobile-first** approach
- Use **dark mode** support with `dark:` prefix
- Keep class names **organized** (layout → spacing → colors → misc)
- Extract repeated patterns into **components**

### Naming Conventions

- **Components**: PascalCase (e.g., `CodeEditor.tsx`)
- **Files**: kebab-case (e.g., `code-editor.tsx`)
- **Functions**: camelCase (e.g., `handleSubmit`)
- **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_FILE_SIZE`)
- **Interfaces**: PascalCase with "Props" suffix (e.g., `CodeEditorProps`)

---

## 🧪 Testing

### Manual Testing

Before submitting a PR:

1. **Test in multiple browsers** (Chrome, Firefox, Safari)
2. **Test responsive design** (mobile, tablet, desktop)
3. **Test edge cases** (empty states, error states)
4. **Test integrations** (APIs, blockchain, AI features)
5. **Test performance** (load times, render performance)

### Automated Testing (Coming Soon)

We're working on adding automated tests. In the meantime:

- Manually test your changes thoroughly
- Document test cases in your PR
- Consider edge cases and error handling

---

## 💬 Community

### Getting Help

- **GitHub Issues**: [Ask questions](https://github.com/mrbrightsides/devarsenal/issues)
- **Telegram**: [@khudriakhmad](https://t.me/khudriakhmad)
- **Discord**: [@khudri_61362](https://discord.com/channels/@khudri_61362)
- **Email**: [support@elpeef.com](mailto:support@elpeef.com)

### Joining Discussions

- Review open issues and PRs
- Share ideas and feedback
- Help other contributors
- Participate in roadmap discussions

### Recognition

Contributors will be:
- Listed in release notes
- Credited in the README
- Recognized in our community channels

---

## 🎯 Areas We Need Help With

Looking to contribute but not sure where to start? Here are some areas we'd love help with:

### High Priority
- 🐛 Bug fixes and stability improvements
- ♿ Accessibility enhancements
- 📱 Mobile responsiveness improvements
- 🌐 Internationalization (i18n) support
- 🧪 Test coverage

### Features
- 🔌 New language support
- 🎨 Additional editor themes
- 📦 More package templates
- 🤖 Enhanced AI capabilities
- ⛓️ Extended blockchain integrations

### Documentation
- 📖 API documentation
- 📝 Tutorial videos or guides
- 🌍 Translations
- 📊 Architecture diagrams
- 💡 Best practices guides

---

## 🏆 Contributor Recognition

All contributors will be recognized in our [Contributors](https://github.com/mrbrightsides/devarsenal/graphs/contributors) page and in release notes.

### Contribution Levels

- **🌟 Star Contributor**: 10+ merged PRs
- **⚔️ Arsenal Warrior**: 5-9 merged PRs  
- **🛡️ Shield Guardian**: 3-4 merged PRs
- **🎯 Marksman**: 1-2 merged PRs

---

## 📄 License

By contributing to Dev Arsenal, you agree that your contributions will be licensed under the **MIT License**.

---

## 🙏 Thank You!

Thank you for taking the time to contribute to Dev Arsenal! Every contribution, no matter how small, helps make this project better for the entire developer community.

**Let's build something amazing together!** ⚔️🔥

---

<div align="center">

## Questions?

Feel free to reach out if you have any questions about contributing!

[📧 Email](mailto:support@elpeef.com) • [💬 Telegram](https://t.me/khudriakhmad) • [🎮 Discord](https://discord.com/channels/@khudri_61362)

**Made with ❤️ for the Dev Arsenal community**

</div>
