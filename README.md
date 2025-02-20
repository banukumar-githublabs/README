Web Scraping & Hosting with Docker

Overview

This project demonstrates how to use Node.js with Puppeteer for web scraping and Python (Flask) for hosting scraped content inside a Docker container.

## Prerequisites

Ensure you have Docker installed. If not, install it using the following commands:

curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh

# Project Structure

This project consists of the following files:

app.py – Flask app to serve scraped data.

scrape.js – Node.js script to scrape website data.

package.json – Dependencies for the Node.js scraper.

requirements.txt – Python dependencies.

Dockerfile – Multi-stage build for the application.

# Building the Docker Image

To build the Docker image, run:

docker build -t my-scraper-image .

# Running the Container

Start the container and expose it on port 5000:

docker run -p 5000:5000 my-scraper-image

# Passing a URL for Scraping

Specify a URL by passing an environment variable during container execution:

docker run -p 5000:5000 -e SCRAPE_URL=https://example.com my-scraper-image

# Accessing the Scraped Data

Once the container is running, access the scraped data via:

http://<your-server-ip>:5000

For example:

http://172.31.3.154:5000

This will return a JSON response containing the scraped content:

{
  "heading": "Example Domain",
  "title": "Example Domain"
}

# Stopping & Restarting the Container

To stop the running container:

docker ps # List running containers
docker stop <container_id>

# To restart the container with a new URL:

docker run -p 5000:5000 -e SCRAPE_URL=https://newwebsite.com my-scraper-image

# Environment Variables

SCRAPE_URL: The URL to be scraped. This variable is required.

PORT: The port number to use for the Flask server. Default is 5000.

# Scraping Details

The scraper uses Puppeteer to load the webpage and extract the title and heading.

The scraped data is stored in a JSON file named scraped_data.json.

# Docker Image Details

The Docker image is built using a multi-stage build process.

The first stage uses the node:18-slim image to install dependencies and run the scraper.

The second stage uses the python:3.10-slim image to install dependencies and run the Flask server.

# Security Considerations

Ensure that the SCRAPE_URL variable is set to a trusted URL to avoid potential security vulnerabilities.

Use a secure connection (HTTPS) when accessing the scraped data.

# Troubleshooting

If the scraper fails, check the Chromium installation inside the Node.js stage.

Use docker logs <container_id> to view container logs.

If you can't access the scraped data externally, ensure your firewall rules or security groups allow inbound traffic on port 5000.


