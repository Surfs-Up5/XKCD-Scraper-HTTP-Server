**#Project 1 – XKCD Server**

<u>##Overview<u>

The XKCD Server is a Golang-based program that downloads and serves XKCD comics via an HTTP REST API. It demonstrates the use of Go, Git, Docker, HTTP servers, multithreading, unit testing, and Postman.
The project started as a simple downloader, then was extended, refactored, and dockerized — reflecting real-world software development practices.

<u>##Tools and Technologies<u>

Golang – Core programming language for development.

Git & GitHub – Version control and collaboration.

VSCode IDE – Development environment with debugging tools.

Docker – Deployment and containerization.

HTTP / REST API – For web server communication.

Postman / curl – For testing API endpoints.

Unit Testing (Go test) – To ensure code correctness.


##Project Versions

<u>###Version 1 – Initial Downloader<u>


Downloads all comics from XKCD

Skips already downloaded comics on reruns.

Demonstrates file I/O and HTTP handling in Go.


<u>###Version 2 – CLI Interface<u>


Added command-line flags:

--version – Display program version.

--parser=regex/html – Choose between HTML parsing methods.

--download-all – Force full download regardless of existing files.

By default, the program stops when it encounters an already downloaded comic and parses data using JSON.

Built using Go’s flag package.


<u>###Version 3 – Multithreading<u>


Utilizes Goroutines to download multiple comics simultaneously.

Flag: --threads=<n> sets number of concurrent downloads (default 3).

Demonstrates Go’s concurrency model and performance benefits.


<u>###Version 4 – XKCD Server (HTTP Server)<u>


Transforms the CLI tool into a web-accessible API server.

Implements REST API endpoints:

Method	Endpoint	Description
GET	/comic/{id}	Returns JSON on comic download status. ({"downloaded": true/false, "isDownloading": true/false})
POST	/comic/{id}	Triggers the download of a specific comic.
GET	/download/{id}	Returns the actual comic image if available, else 404.

Supports both manual and client-side requests.

Designed for testing with Postman and curl.

##Testing

Unit tests written using Go’s built-in testing package.

Run tests with:

go test ./...


Tests validate functionality, document behavior, and prevent regressions during refactors.

##Setup & Run (Locally)

1. Clone repository
git clone https://github.com/<username>/xkcd-server.git
cd xkcd-server

2. Build
go build -o xkcd-server main.go

3. Run with defaults
./xkcd-server

# Example: Run with CLI options
./xkcd-server --threads=5 --download-all

##Run via Docker

###Build Docker image
docker build -t xkcd-server .

###Run container
docker run -d -p 8080:8080 xkcd-server


Server will be available at http://localhost:8080.

##API Using Postman or curl

###Check if a comic exists
curl http://localhost:8080/comic/1234

###Request a comic download
curl -X POST http://localhost:8080/comic/1234

###Get downloaded comic
curl http://localhost:8080/download/1234

🔗 Cross-Platform Testing

Tested on Windows and Linux (Ubuntu/Mint) via VirtualBox.
