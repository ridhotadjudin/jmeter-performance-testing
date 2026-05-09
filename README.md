# 🚀 JMeter Performance Testing — Reqres API

![License](https://img.shields.io/badge/License-MIT-green.svg)

![Performance Tests](https://github.com/ridhotadjudin/jmeter-performance-testing/actions/workflows/performance-test.yml/badge.svg)

Automated **performance and load testing** suite for the [Reqres](https://reqres.in) REST API, built with **Apache JMeter** and **Maven**. Designed as a portfolio project demonstrating end-to-end API performance testing skills.

---

## 📋 Table of Contents

- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [How to Run](#-how-to-run)
- [Test Scenarios](#-test-scenarios)
- [Sample Results](#-sample-results)
- [Project Structure](#-project-structure)
- [CI/CD](#-cicd)

---

## 🛠 Tech Stack

| Tool | Purpose |
|------|---------|
| [Apache JMeter 5.6+](https://jmeter.apache.org/) | Load & performance test engine |
| [Maven 3.8+](https://maven.apache.org/) | Build automation & test execution |
| [jmeter-maven-plugin](https://github.com/jmeter-maven-plugin/jmeter-maven-plugin) | Run JMeter tests from Maven |
| [Java 17+](https://adoptium.net/) | Runtime |
| [GitHub Actions](https://github.com/features/actions) | CI/CD pipeline |

---

## ✅ Prerequisites

- **Java JDK 17+** — `java -version`
- **Apache Maven 3.8+** — `mvn -version`
- **Apache JMeter 5.6+** *(only for GUI mode)* — `jmeter --version`

---

## ▶ How to Run

### 1. Get your API key (required)

ReqRes now requires an API key. Get yout free key at [app.reqres.in/api-keys](https://app.reqres.in/api-keys).

### 2. CLI — Maven (Recommended)

```bash
# Run all JMeter tests and generate HTML report
mvn clean verify

# Override thread count and ramp-up from CLI
mvn clean verify -Dthreads=100 -Drampup=20 -Diterations=5
```

Reports are generated in `target/jmeter/reports/`.

### GUI — JMeter Desktop

1. Open JMeter: `jmeter.bat` (Windows) or `jmeter.sh` (macOS/Linux)
2. **File → Open** → `src/test/jmeter/reqres-api-load-test.jmx`
3. Click the green **Start** button ▶

---

## 🧪 Test Scenarios

| # | Method | Endpoint | Description | Expected Status |
|---|--------|----------|-------------|-----------------|
| 1 | `GET` | `/api/users?page=2` | List users (paginated) | `200 OK` |
| 2 | `GET` | `/api/users/2` | Get single user by ID | `200 OK` |
| 3 | `POST` | `/api/users` | Create user (CSV-driven) | `201 Created` |
| 4 | `PUT` | `/api/users/2` | Update existing user | `200 OK` |

### Load Profile

| Parameter | Value |
|-----------|-------|
| Virtual Users (Threads) | 50 |
| Ramp-Up Period | 10 seconds |
| Iterations per Thread | 2 |
| Total Requests | 500 (50 users × 2 iterations × 5 requests) |

### Features

- **CSV Data-Driven Testing** — User creation & update requests are parameterized via `user-data.csv`
- **Response Assertions** — HTTP status codes and JSON path validations
- **HTTP Request Defaults** — Centralized base URL and timeout configuration
- **Multiple Listeners** — Summary Report, Aggregate Report, View Results Tree

---

## 📊 Sample Results

> *Results will vary based on network conditions and server load.*

| Request | Samples | Avg (ms) | Min (ms) | Max (ms) | Error % | Throughput |
|---------|---------|----------|----------|----------|---------|------------|
| GET - List Users | 100 | 250 | 180 | 520 | 0.00% | 8.5/s |
| GET - Single User | 100 | 230 | 170 | 480 | 0.00% | 8.8/s |
| POST - Create User | 100 | 280 | 200 | 600 | 0.00% | 7.9/s |
| PUT - Update User | 100 | 260 | 190 | 550 | 0.00% | 8.2/s |

---

## 📁 Project Structure

```
jmeter-performance-testing/
├── .github/
│   └── workflows/
│       └── performance-test.yml      # GitHub Actions CI/CD pipeline
├── src/
│   └── test/
│       └── jmeter/
│           ├── reqres-api-load-test.jmx   # JMeter test plan
│           └── user-data.csv              # CSV data for parameterized tests
├── .gitignore
├── pom.xml                                # Maven config with jmeter-maven-plugin
└── README.md
```

---

## 🔄 CI/CD

The project includes a **GitHub Actions** workflow (`.github/workflows/performance-test.yml`) that:

1. Triggers on **push to main**, **pull requests**, or **manual dispatch**
2. Sets up **JDK 17** with Maven caching
3. Runs `mvn clean verify` to execute all JMeter tests
4. **Archives** the HTML report and JTL results as build artifacts

---

## Author

**Ridho Tadjudin** — QA Engineer

- 🌐 Website: [ridhotadjudin.id](https://ridhotadjudin.id)
- 💻 GitHub: [@ridhotadjudin](https://github.com/ridhotadjudin)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Built with ☕ and <a href="https://docs.oracle.com/">Java</a>
</p>
