---
title: Ch11 05 Pip
date: 2025-12-27
author: Your Name
cell_count: 36
score: 35
---

# Python pip

Package management with Python's official installer, `pip`.

## 1. What is pip



```python
pip --version

```

`pip` installs, upgrades, and manages packages from PyPI.

## 2. Installing a Package



```python
pip install requests

```

Downloads and installs a package and its dependencies.

## 3. Upgrading a Package



```python
pip install --upgrade requests

```

Ensures the latest stable version is installed.

## 4. Uninstalling a Package



```python
pip uninstall requests

```

Removes the package and related files.

## 5. Listing Installed Packages



```python
pip list

```

Displays all packages in the environment.

## 6. Viewing Package Information



```python
pip show requests

```

Shows version, location, and dependencies.

## 7. Installing Specific Package Version



```python
pip install numpy==1.24.0

```

Locks installation to an exact version for reproducibility.

## 8. Using requirements.txt



```python
pip install -r requirements.txt

```

Example `requirements.txt`:
```
flask==2.2.3
requests>=2.25
numpy
```

Essential for dependency management in team environments.

## 9. Freezing Dependencies



```python
pip freeze > requirements.txt

```

Exports exact versions for deployment or CI/CD.

## 10. Enterprise Deployment Example



```python
# Step 1: Create virtual environment
python -m venv venv

# Step 2: Activate environment
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows

# Step 3: Install dependencies
pip install -r requirements.txt

```

Ensures isolated, repeatable, production-grade deployments.

## Common pip Commands Reference
- `pip install package` → install package
- `pip uninstall package` → remove package
- `pip list` → show installed packages
- `pip show package` → package details
- `pip freeze` → output dependency list
- `pip install --upgrade package` → update package

## pip vs Conda
- `pip`: Python-only, PyPI-based, lightweight package manager.
- `conda`: Environment + package manager for multi-language stacks, data-science focused.

## Best Practices
- Always use virtual environments.
- Lock versions for production.
- Keep `requirements.txt` updated.
- Avoid global installs; use virtual envs or `--user`.
- Integrate pip steps into CI/CD.

## Common Issues & Solutions
- Permission denied → use virtual env or `pip install --user`.
- Version conflicts → isolate environments.
- Slow installs → use cached wheels or mirrors.
- Dependency hell → define strict version constraints.


---
**Score: 35**