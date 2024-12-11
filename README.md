
# Semgrep Custom Rules for Code Vulnerability Detection

This repository contains custom Semgrep rules made by team Vidhyadhar during SIH for detecting vulnerabilities in C and C++ code. The custom rules are applied to source files to identify potential security issues such as command injection, unchecked memory allocation, and unsafe API calls.

## Overview

Semgrep is a static analysis tool that scans code for patterns and vulnerabilities based on predefined or custom rules. In this project, we have created custom rules to scan C source files for potential security flaws. This README explains how to set up and run Semgrep using these custom rules to analyze your codebase.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Docker**: Semgrep runs inside a Docker container, so Docker must be installed and running on your machine.
- **Semgrep Docker Image**: We use the official `returntocorp/semgrep` image to run Semgrep scans.

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/semgrep-custom-rules.git
cd semgrep-custom-rules
```

### 2. Prepare the Directory for Custom Rules

The custom Semgrep rules are located in the `semgrep-rules` folder. Each rule is defined in a `.yaml` file under the `semgrep-rules/c/` directory. These rules check for common security vulnerabilities in C code, such as:

- **Command Injection**: Detects potential command injection vulnerabilities.
- **Unchecked Memory Allocation**: Identifies cases where memory allocation functions (like `malloc`, `calloc`, etc.) are not checked for failure.
- **Unsafe API Calls**: Detects unsafe or insecure API calls that can lead to security issues.

### 3. Prepare Your Code to Scan

Make sure the code you want to analyze is in the `Test` folder. This folder will be mounted to the container to be analyzed by Semgrep.

### 4. Running Semgrep with Custom Rules

To scan your source files using the custom rules, run the following Docker command:

```bash
docker run --rm \
  -v /path/to/semgrep-rules:/rules \
  -v /path/to/Test:/source \
  returntocorp/semgrep semgrep --config /rules/c /source
```

Replace `/path/to/semgrep-rules` with the path to your custom rules directory and `/path/to/Test` with the path to your source code directory.

#### Example:

```bash
docker run --rm \
  -v /mnt/c/Users/aasth/OneDrive/Desktop/CustomCaseD/semgrep-rules:/rules \
  -v /mnt/c/Test:/source \
  returntocorp/semgrep semgrep --config /rules/c /source
```

### Explanation of Command

- `--rm`: Removes the container after the scan is completed.
- `-v /path/to/semgrep-rules:/rules`: Mounts the `semgrep-rules` directory (where the `.yaml` rules are stored) into the Docker container.
- `-v /path/to/Test:/source`: Mounts the `Test` directory (where the source code files are located) into the Docker container.
- `semgrep --config /rules/c /source`: Runs Semgrep using the custom rules defined in `/rules/c` to scan the source files located in `/source`.

## Results

After running the command, Semgrep will output any findings related to vulnerabilities in your code. Each finding will include the line of code that violates the rule, along with an explanation of the issue.

## Modifying Rules

If you want to customize the rules, you can modify the `.yaml` files located in the `semgrep-rules/c` directory. Each rule file contains the pattern and logic for detecting specific vulnerabilities. You can add new rules or modify existing ones to better suit your needs.

## Conclusion

By using Semgrep with custom rules, you can automate the detection of security vulnerabilities in your codebase, making it easier to maintain secure and reliable software. This setup allows you to integrate static code analysis into your development workflow and ensure your code is free from common security flaws.
