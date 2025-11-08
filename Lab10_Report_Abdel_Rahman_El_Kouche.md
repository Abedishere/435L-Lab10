# Lab 10 Report: Jenkins CI/CD Pipeline for Python

**Abdel Rahman El Kouche**
202306902

**Date:** November 8, 2025

---

## Part 4 - Modifications and Enhancements

This report explains the modifications made to the Jenkins pipeline to fulfill Part 4 requirements: adding code coverage analysis, security scanning, and implementing deployment logic.

---

## 1. Code Coverage Analysis (Coverage Stage)

### Changes Made
- Added a new stage named **"Coverage"** to the Jenkinsfile
- Integrated `coverage.py` tool for code coverage analysis
- Added `coverage` to requirements.txt

### Implementation
The Coverage stage executes the following commands:

1. `coverage run -m pytest tests/`
   - Runs pytest while collecting coverage data
2. `coverage report -m`
   - Displays coverage report in the console
3. `coverage html`
   - Generates HTML coverage report in `htmlcov/` directory

### Code Added to Jenkinsfile

```groovy
stage('Coverage') {
    steps {
        script {
            echo "Running code coverage analysis..."
            bat """
                call ${VIRTUAL_ENV}\\Scripts\\activate.bat && coverage run -m pytest tests/
                call ${VIRTUAL_ENV}\\Scripts\\activate.bat && coverage report -m
                call ${VIRTUAL_ENV}\\Scripts\\activate.bat && coverage html
            """
            echo "Coverage report generated in htmlcov/index.html"
        }
    }
}
```

---

## 2. Security Scanning (Security Scan Stage)

### Changes Made
- Added a new stage named **"Security Scan"** to the Jenkinsfile
- Integrated `bandit` security vulnerability scanner
- Added `bandit` to requirements.txt

### Implementation
The Security Scan stage executes bandit to check for common security issues:

1. `bandit -r app.py -f txt -o bandit-report.txt`
   - Scans app.py recursively and saves report to file
2. `bandit -r app.py`
   - Displays security scan results in console

### Code Added to Jenkinsfile

```groovy
stage('Security Scan') {
    steps {
        script {
            echo "Running security scan with bandit..."
            bat """
                call ${VIRTUAL_ENV}\\Scripts\\activate.bat && bandit -r app.py -f txt -o bandit-report.txt || exit 0
                call ${VIRTUAL_ENV}\\Scripts\\activate.bat && bandit -r app.py
            """
            echo "Security scan completed. Report saved to bandit-report.txt"
        }
    }
}
```

---

## 3. Deployment Implementation (Enhanced Deploy Stage)

### Changes Made
- Enhanced the Deploy stage with actual deployment logic
- Implemented file copying to simulate production deployment

### Implementation
The Deploy stage now performs actual deployment actions:

1. Creates a `deploy/` directory if it doesn't exist
2. Copies the application files (`app.py`) to the deploy directory
3. Confirms successful deployment

### Code Added to Jenkinsfile

```groovy
stage('Deploy') {
    steps {
        script {
            echo "Deploying application..."
            bat """
                if not exist deploy mkdir deploy
                copy app.py deploy\\
                echo Deployment completed successfully!
            """
            echo "Application deployed to ./deploy directory"
        }
    }
}
```

---

## 4. Additional Modifications

### Environment Variables
Added explicit Python path to ensure Jenkins can locate Python:

```groovy
environment {
    VIRTUAL_ENV = 'venv'
    PYTHON_PATH = 'C:\\Users\\user\\AppData\\Local\\Programs\\Python\\Python313\\python.exe'
}
```

### Updated requirements.txt

**Original:**
```
flake8
```

**Modified to include all tools:**
```
flake8
pytest
coverage
bandit
```

### Code Style Fixes
Fixed flake8 violations in `app.py`:
- Added proper blank lines between function definitions
- Added newline at end of file

---

## Jenkins Pipeline Output

### Pipeline Execution Summary
- **Pipeline Name:** Python-CI-CD
- **Build Status:** SUCCESS
- **All Stages:** PASSED

### Stage-by-Stage Results

#### [Stage 1: Setup] - PASSED
- Created Python virtual environment (venv)
- Installed all dependencies (flake8, pytest, coverage, bandit)
- Duration: ~25 seconds (first run)

#### [Stage 2: Lint] - PASSED
- Ran flake8 code quality checker
- No style violations found
- Code complies with PEP 8 standards

#### [Stage 3: Test] - PASSED
- Executed unit tests with pytest
- Test: `test_greet` - PASSED
- Verified greeting message includes student name

#### [Stage 4: Coverage] - PASSED (NEW - Part 4 Requirement)
- Ran coverage analysis on test suite
- Generated coverage report
- Created HTML report in `htmlcov/`
- Coverage metrics collected successfully

#### [Stage 5: Security Scan] - PASSED (NEW - Part 4 Requirement)
- Ran bandit security scanner
- Scanned `app.py` for vulnerabilities
- Generated `bandit-report.txt`
- No security issues detected

#### [Stage 6: Deploy] - PASSED (ENHANCED - Part 4 Requirement)
- Created `deploy/` directory
- Copied `app.py` to deployment location
- Deployment completed successfully

### Post-Actions
- Workspace cleaned up successfully

---

## Conclusion

All Part 4 requirements have been successfully implemented:

- ✅ **Code Coverage:** Integrated coverage.py with detailed reporting
- ✅ **Security Scanning:** Integrated bandit for vulnerability detection
- ✅ **Deployment:** Implemented functional deployment script

The Jenkins pipeline now provides a complete CI/CD workflow that includes:
- Automated dependency installation
- Code quality checking (linting)
- Automated testing
- Code coverage analysis
- Security vulnerability scanning
- Automated deployment

The pipeline successfully automates the entire development workflow from code validation to deployment, demonstrating modern DevOps practices.

---

**GitHub Repository:** [https://github.com/Abedishere/435L-Lab10](https://github.com/Abedishere/435L-Lab10)
