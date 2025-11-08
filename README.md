# Jenkins CI/CD Pipeline for Python - Lab 10

**Student:** Abdel Rahman El Kouche
**Course:** Software Tools Lab - Fall 2025-2026

## Project Overview

This project demonstrates a complete CI/CD pipeline using Jenkins for a Python application. The pipeline includes automated testing, code coverage analysis, security scanning, and deployment.

## Pipeline Stages

1. **Setup** - Creates virtual environment and installs dependencies
2. **Lint** - Runs flake8 for code style checking
3. **Test** - Executes unit tests with pytest
4. **Coverage** - Generates code coverage reports using coverage.py
5. **Security Scan** - Performs security vulnerability scanning with bandit
6. **Deploy** - Deploys the application (simulated deployment to ./deploy directory)

## Project Structure

```
435Lab10/
├── app.py                                    # Main application file
├── tests/                                    # Test directory
│   ├── __init__.py
│   └── test_app.py                          # Unit tests
├── requirements.txt                          # Python dependencies
├── Jenkinsfile_Abdel_Rahman_El_Kouche      # Jenkins pipeline configuration
├── .gitignore                               # Git ignore rules
└── README.md                                # This file
```

## Requirements

- Python 3.x
- Jenkins with Pipeline plugin
- Git

## Dependencies

- flake8 - Code linting
- pytest - Testing framework
- coverage - Code coverage analysis
- bandit - Security vulnerability scanner

## Running Locally

1. Create virtual environment:
   ```bash
   python -m venv venv
   ```

2. Activate virtual environment:
   ```bash
   # Windows
   venv\Scripts\activate

   # Linux/Mac
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run tests:
   ```bash
   pytest tests/
   ```

5. Check coverage:
   ```bash
   coverage run -m pytest tests/
   coverage report -m
   ```

6. Run security scan:
   ```bash
   bandit -r app.py
   ```

## Jenkins Setup

1. Create a new Pipeline job in Jenkins named `Python-CI-CD`
2. Configure the job to use this Git repository: https://github.com/Abedishere/435L-Lab10
3. Set the pipeline script path to: `Jenkinsfile_Abdel_Rahman_El_Kouche`
4. Run the pipeline

## Changes Made for Exercise (Part 4)

### Added Coverage Stage:
- Integrated coverage.py tool
- Generates detailed coverage reports
- Creates HTML coverage report in htmlcov/ directory

### Added Security Scan Stage:
- Integrated bandit security scanner
- Checks for common security vulnerabilities
- Generates security report (bandit-report.txt)

### Enhanced Deployment Stage:
- Implemented basic deployment script
- Copies application files to deployment directory
- Simulates production deployment process

## Pipeline Output

All stages are expected to pass:
- ✓ Setup - Virtual environment created, dependencies installed
- ✓ Lint - Code style checks passed
- ✓ Test - All unit tests passed
- ✓ Coverage - Code coverage report generated
- ✓ Security Scan - No vulnerabilities found
- ✓ Deploy - Application deployed successfully

## Repository

GitHub: https://github.com/Abedishere/435L-Lab10
