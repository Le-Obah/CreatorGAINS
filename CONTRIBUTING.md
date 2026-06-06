# Contributing to CreatorGAINS

Thank you for your interest in contributing to CreatorGAINS!

## Getting Started

1. Fork the repository
2. Clone your fork: `git clone https://github.com/YOUR_USERNAME/CreatorGAINS.git`
3. Create a feature branch: `git checkout -b week-X-feature-name`
4. Make your changes
5. Commit with clear messages
6. Push to your fork
7. Open a Pull Request

## Branch Naming Convention

- `week-X-feature-name` - Feature development
- `bugfix/issue-number` - Bug fixes
- `docs/topic` - Documentation updates

Example: `week-2-authentication`, `bugfix/login-error`, `docs/api`

## Commit Messages

Follow this format:

```
[Week X] Feature: Brief description (50 chars max)

Detailed explanation of changes (if needed)
- Bullet point 1
- Bullet point 2
```

## Code Standards

### JavaScript/TypeScript
- Use ESLint configuration
- Use Prettier for formatting
- Write meaningful variable names
- Add JSDoc comments for functions

```javascript
/**
 * Authenticates user with email and password
 * @param {string} email - User email
 * @param {string} password - User password
 * @returns {Promise<Object>} User object with token
 */
async function authenticateUser(email, password) {
  // Implementation
}
```

## Git Workflow

```
main (stable)
  ↑
  ├── week-X-feature (development)
  │   ├── sub-feature-1
  │   └── sub-feature-2
  │
  └── bugfix/issue (hotfixes)
```

## Testing

- Write unit tests for new features
- Ensure 80%+ code coverage
- Run tests: `npm test`
- Add integration tests for critical paths

## Documentation

- Update README.md for major changes
- Add comments for complex logic
- Update API docs for endpoint changes
- Add examples for new features

## Pull Request Process

1. Ensure all tests pass: `npm test`
2. Update documentation as needed
3. Add screenshots/videos for UI changes
4. Link related issues in PR description
5. Request review from team members
6. Address feedback and re-request review
7. Squash commits if needed before merge

## Code Review Guidelines

When reviewing:
- Check code quality and consistency
- Verify tests are included
- Ensure documentation is updated
- Test locally if possible
- Provide constructive feedback

## Questions?

- Open an issue for bugs
- Start a discussion for ideas
- Check existing documentation
- Contact team leads for guidance

Thanks for contributing! 🚀
