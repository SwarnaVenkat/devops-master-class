# -------- Stage 1: Builder --------
FROM python:3.10-alpine AS builder
 
WORKDIR /app
 
# Install build dependencies (if needed for some Python packages)
RUN apk add --no-cache gcc musl-dev libffi-dev
 
# Copy only requirements first (better caching)
COPY requirements.txt .
 
# Install dependencies into a custom folder
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt
 
 
# -------- Stage 2: Final Image --------
FROM python:3.10-alpine
 
WORKDIR /app
 
# Copy installed dependencies from builder stage
COPY --from=builder /install /usr/local
 
# Copy application code
COPY . /app
 
EXPOSE 4000
 
CMD ["python", "./launch.py"]
