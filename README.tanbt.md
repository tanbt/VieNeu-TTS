# Run with Docker - for CPU, PyTorch loaded
```
docker compose up --build -d
```

# Deploy the built image to Docker Hub

The Compose file builds the image directly as `tanbui/vieneu-tts:cpu`. To publish
it to Docker Hub, build and push it.

1. Log in to Docker Hub (only needed once per machine):
   ```
   docker login
   ```

2. Build the image:
   ```
   docker compose build
   ```

3. Push the image to Docker Hub:
   ```
   docker push tanbui/vieneu-tts:cpu
   ```

The image is now available at `docker.io/tanbui/vieneu-tts:cpu`.

# Run the app from the Docker Hub image

On any machine with Docker installed, you can run the published image without
cloning the repository or rebuilding.

Quick start with `docker run`:
```
docker run -d \
  --name vieneu-tts-web \
  -p 7860:7860 \
  -e GRADIO_SERVER_NAME=0.0.0.0 \
  -e GRADIO_SERVER_PORT=7860 \
  -v huggingface_cache:/root/.cache/huggingface \
  -v "$(pwd)/output_audio:/workspace/output_audio" \
  tanbui/vieneu-tts:cpu
```

Then open http://localhost:7860.

Or with Docker Compose — this repo's `docker-compose.yml` already uses the
`tanbui/vieneu-tts:cpu` image, so you can pull the online image and run it
without rebuilding:
```
docker compose pull
docker compose up -d
```