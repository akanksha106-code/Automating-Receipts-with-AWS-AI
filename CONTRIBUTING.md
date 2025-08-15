# Contributing

Thanks for contributing! Please follow these steps:

1. Fork the repository and create your branch from `main`.
2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv .venv && .venv/Scripts/activate
   pip install -r requirements.txt
   pip install -U black isort flake8
   ```
3. Run linters before committing:
   ```bash
   black . && isort . && flake8 .
   ```
4. Add tests if applicable and update documentation.
5. Open a Pull Request with a clear description.