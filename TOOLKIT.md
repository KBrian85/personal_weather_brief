# Personal Daily Weather Brief in Go
**Toolkit Document (Capstone)**

## 1. Title & Objective
**Technology Choice:** Go (Golang) + Open-Meteo weather API (optional LLM tone polishing).  
**Justification:** Go is ideal for lightweight CLI tools with strong HTTP/JSON support and easy deployment as a single binary.  
**End Goal:** A minimal CLI that takes a city name and generates an actionable brief for tomorrow (console + Markdown).

## 2. Quick Summary of the Technology
**Definition:** Go is a compiled, statically typed language designed for simplicity, performance, and reliability.  
**Use Cases:** CLIs, backend APIs/microservices, automation tools, cloud-native apps.  
**Real-World Example:** Many modern developer tools and cloud utilities are built in Go due to speed and portability.

## 3. System Requirements
- OS: Windows/macOS/Linux
- Go 1.20+ (1.21+ recommended)
- Editor: VS Code + Go extension
- Internet for live forecast (optional if using `--mock`)
- Optional plotting: Python 3 + matplotlib

## 4. Installation & Setup Instructions
```bash
go mod tidy
go run ./cmd/brief --city "Nairobi"
```
Offline demo:
```bash
go run ./cmd/brief --city "Nairobi" --mock
```

## 5. Minimal Working Example (MWE)
The MWE is the CLI command above. Expected output: a brief in bullets plus `brief.md`.

## 6. AI Prompt Journal
Prompt style used in code for optional LLM enhancement:
- “Use ONLY the JSON input. Do not invent numbers or conditions. Return 5–7 bullet points plus one short closing line.”
Reflection: Adding strict constraints improved accuracy and reduced hallucinations.

## 7. Common Issues & Fixes
- City not found: try “City, Country”
- Network issues: use `--mock`
- Missing Go: install and verify `go version`

## 8. References
- Go documentation (official)
- Open-Meteo docs (forecast + geocoding)
