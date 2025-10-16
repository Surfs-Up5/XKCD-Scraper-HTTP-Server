# XKCD Scraper HTTP Server

A Golang-based HTTP server that scrapes XKCD comics, serves them via a REST API, and supports multi-threaded downloads using Goroutines.

## Features

- Downloads XKCD comics and stores them locally.
- REST API endpoints:
  - `GET /comic/{id}` – Check if a comic is downloaded or currently downloading.
  - `POST /comic/{id}` – Request a comic to be downloaded.
  - `GET /download/{id}` – Download the comic image if available.
- Multi-threaded downloads using Goroutines.
- Supports CLI flags for version info and server mode.

## Requirements

- Go 1.25+
- Docker (optional, for containerization)

## Setup & Run

### Locally

1. Clone the repository:
   
   git clone https://github.com/Surfs-Up5/XKCD-Scraper-HTTP-Server.git
   cd Project-1

2. Install dependencies:

   go mod download

3. Run the server:

   go run Project1.go --server

   The server will start on: http://localhost:8080

   API Endpoints:
  - Check comic status: http://localhost:8080/comic/1
  - Download comic: http://localhost:8080/download/1

### Docker Deployment

1. Build the Docker image:
   
  docker build -t xkcd-server ./Project-1

2. Run the container:
  
  docker run -p 8080:8080 xkcd-server

  Comics are saved in the comics/ folder inside the container. Use volumes to persist locally.

### Using Docker Compose
  If both server and client are defined in the same docker-compose.yml, run:

  docker compose up --build

## Notes
- Comics will be saved to the `comics/` folder.
- Works both locally and in Docker environments.
- Logs server activity to the console.



  
   

  



   
