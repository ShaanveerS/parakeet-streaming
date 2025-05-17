# Parakeet Realtime Transcription Server

This project provides a real-time audio transcription server using NVIDIA's Parakeet ASR model. It can be run directly with Python or using Docker.

## Installation & Running

There are two main ways to run the server:

### Option 1: Using Docker

This is the easiest way to get the server running with all its CUDA and NeMo dependencies.

1. **Prerequisites:**

   * Docker installed
2. **Build and Run with Docker Compose:**
   The `docker-compose.yaml` file is configured to use `dev.Dockerfile`.

   ```bash
   docker-compose up --build
   ```

   This will:

   * Build the Docker image defined in `dev.Dockerfile`.
   * Start the server.
   * The server will be accessible on `http://localhost:9090` (host) which maps to port `9000` (container).
   * The WebSocket endpoint will be `ws://localhost:9090/transcribe`.

### Option 2: Manual Python Setup

1. **Clone the repository (if applicable):**

   ```bash
   https://github.com/ShaanveerS/parakeet-streaming.git
   cd parakeet-realtime-server 
   ```
2. **Create and activate a virtual environment:**

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. **Install Python dependencies:**

   ```bash
   pip install -r requirements.txt 
   ```
4. **Running the Server (without Docker):**
   The `server.py` expects to run with Uvicorn. The Dockerfiles use port `9000`.

   ```bash
   uvicorn server:app --host 0.0.0.0 --port 9000
   ```

## Running the Client Example

(Ensure the server is running, either via Docker or manually)

```bash
python client_example.py --url ws://localhost:PORT/transcribe
```

Replace `PORT` with `9090` if using the Docker Compose setup, or `9000` if running the server manually (default).
This will use your microphone to stream audio and print transcriptions. Press `Ctrl+C` to stop.
