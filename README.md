# XKCD Server
## Overview

The XKCD Server is a Golang-based program that downloads and serves XKCD comics via an HTTP REST API.
It demonstrates the use of Go, Git, Docker, HTTP servers, multithreading, unit testing, and Postman.
The project started as a simple downloader, then was extended, refactored, and dockerized — reflecting real-world software development practices.

## Tools and Technologies

Golang – Core programming language for development

Git & GitHub – Version control and collaboration

VSCode IDE – Development environment with debugging tools

Docker – Deployment and containerization

HTTP / REST API – Web server communication

Postman / curl – Testing API endpoints

Unit Testing (Go test) – Ensures code correctness

## Project Versions
### Version 1 – Initial Downloader

Downloads all comics from XKCD

Skips already downloaded comics on reruns

Demonstrates file I/O and HTTP handling in Go

### Version 2 – CLI Interface

Added command-line flags:

--version – Display program version

--parser=regex/html – Choose between HTML parsing methods

--download-all – Force full download regardless of existing files

Defaults:

Stops when encountering an already downloaded comic

Parses data using JSON

Built using Go’s flag package

### Version 3 – Multithreading

Utilizes Goroutines to download multiple comics simultaneously

Flag: --threads= sets number of concurrent downloads (default: 3)

Demonstrates Go’s concurrency model and performance benefits

### Version 4 – XKCD Server (HTTP Server)

Transforms the CLI tool into a web-accessible API server.

REST API Endpoints
Method	Endpoint	Description
GET	/comic/{id}	Returns JSON with comic download status → {"downloaded": true/false, "isDownloading": true/false}
POST	/comic/{id}	Triggers the download of a specific comic
GET	/download/{id}	Returns the actual comic image if available, else 404

Supports both manual and client-side requests

Designed for testing with Postman and curl

## Testing

Unit tests are written using Go’s built-in testing package.

Run tests with:

go test ./...


Tests validate functionality, document behavior, and prevent regressions during refactors.

## Setup & Run (Locally)
### Clone repository
git clone https://github.com/<your-username>/xkcd-server.git
cd xkcd-server

### Build executable
go build -o xkcd-server main.go

### Run with defaults
./xkcd-server

### Example: Run with CLI options
./xkcd-server --threads=5 --download-all

## Run via Docker
### Build Docker Image
docker build -t xkcd-server .

### Run Container
docker run -d -p 8080:8080 xkcd-server


Server will be available at:
http://localhost:8080

## API Usage (Postman / curl)
Check if a comic exists
curl http://localhost:8080/comic/1234

Request a comic download
curl -X POST http://localhost:8080/comic/1234

Get downloaded comic
curl http://localhost:8080/download/1234

## Cross-Platform Testing

Tested on Windows and Linux (Ubuntu/Mint) via VirtualBox.
