# Contributing to NovaGuard AI

First off, thank you for considering contributing to NovaGuard AI! It's people like you that make NovaGuard such a great tool.

## Code of Conduct

This project and everyone participating in it is governed by our Code of Conduct. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues as you might find out that you don't need to create one. When you are creating a bug report, please include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps to reproduce the problem**
- **Provide specific examples to demonstrate the steps**
- **Describe the behavior you observed and what you expected**
- **Include screenshots if relevant**
- **Include your environment details** (OS, Python version, etc.)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, please include:

- **Use a clear and descriptive title**
- **Provide a detailed description of the suggested enhancement**
- **Explain why this enhancement would be useful**
- **List any alternative solutions you've considered**

### Pull Requests

1. Fork the repo and create your branch from `main`
2. If you've added code that should be tested, add tests
3. Ensure the test suite passes
4. Make sure your code follows the project's style guidelines
5. Write a convincing description of your PR

## Development Workflow

### Setup Development Environment

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/novaguard.git
cd novaguard

# Add upstream remote
git remote add upstream https://github.com/original/novaguard.git

# Create a branch
git checkout -b feature/my-feature

# Setup backend
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Setup frontend
cd ../frontend
npm install
```

### Code Style

#### Python (Backend)
- Follow PEP 8
- Use type hints
- Maximum line length: 100 characters
- Use docstrings for all functions and classes
- Run `black` for formatting
- Run `flake8` for linting
- Run `mypy` for type checking

```bash
# Format code
black app/

# Lint code
flake8 app/

# Type check
mypy app/
```

#### TypeScript/Angular (Frontend)
- Follow Angular style guide
- Use TypeScript strict mode
- Use ESLint for linting
- Use Prettier for formatting

```bash
# Lint
npm run lint

# Format
npm run format
```

### Testing

#### Backend Tests
```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app tests/

# Run specific test file
pytest tests/test_waf.py
```

#### Frontend Tests
```bash
# Run unit tests
npm test

# Run e2e tests
npm run e2e
```

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <subject>

<body>

<footer>
```

Types:
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

Examples:
```
feat(waf): add XSS detection algorithm

fix(api): resolve rate limiting issue

docs(readme): update installation instructions
```

### Branch Naming

- Feature: `feature/description-of-feature`
- Bug fix: `fix/description-of-bug`
- Hotfix: `hotfix/description`
- Documentation: `docs/description`

## Project Structure Guidelines

### Backend (FastAPI)

```python
# Good: Type hints and docstrings
async def analyze_request(request: Request) -> ThreatAnalysis:
    """
    Analyze incoming request for security threats.
    
    Args:
        request: FastAPI request object
        
    Returns:
        ThreatAnalysis object containing threat information
        
    Raises:
        ValidationError: If request is malformed
    """
    pass

# Bad: No type hints or docstrings
async def analyze_request(request):
    pass
```

### Frontend (Angular)

```typescript
// Good: Strong typing and documentation
/**
 * Analyzes threat data and returns visualization config
 */
export interface ThreatAnalysis {
  threatLevel: 'low' | 'medium' | 'high' | 'critical';
  detectedThreats: string[];
  timestamp: Date;
}

// Bad: Any types
export interface ThreatAnalysis {
  data: any;
}
```

## ML Model Contributions

When contributing ML models:

1. Document the model architecture
2. Include training scripts and data preprocessing
3. Provide performance metrics (accuracy, precision, recall)
4. Include model evaluation results
5. Explain hyperparameter choices
6. Consider model size and inference time

## Documentation

- Update README.md if needed
- Add inline code comments for complex logic
- Update API documentation (OpenAPI/Swagger)
- Add examples for new features
- Update changelog

## Review Process

1. All submissions require review
2. Address review comments promptly
3. Maintain a clean commit history
4. Ensure CI/CD checks pass
5. Update tests as needed

## Questions?

Feel free to open an issue with the label `question` or reach out to the maintainers.

## Recognition

Contributors will be recognized in:
- CONTRIBUTORS.md file
- Release notes
- Project documentation

Thank you for contributing to NovaGuard AI! 🛡️
