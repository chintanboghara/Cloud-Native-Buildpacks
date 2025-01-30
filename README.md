# Cloud Native Buildpacks

Cloud Native Buildpacks (CNB) transform application source code into OCI-compliant container images in a secure, efficient, and reproducible way-without requiring Dockerfiles.

## Features
- No need for Dockerfiles
- Secure and optimized container images
- Multi-language support (Java, Node.js, Python, Go, etc.)
- Automated dependency management
- Seamless CI/CD integration

## Getting Started

### Prerequisites
Ensure you have the following installed:
- [Docker](https://www.docker.com/)
- [Pack CLI](https://buildpacks.io/docs/tools/pack/)
- A supported builder (e.g., Paketo, Heroku, Google Cloud Buildpacks)

### Build a Node.js Application

1. Create a Node.js project:
   ```sh
   mkdir my-node-app && cd my-node-app
   npm init -y
   npm install express
   ```

2. Create `index.js`:
   ```javascript
   const express = require('express');
   const app = express();
   const port = process.env.PORT || 3000;

   app.get('/', (req, res) => {
       res.send('Hello, Cloud Native Buildpacks!');
   });

   app.listen(port, () => {
       console.log(`Server running on port ${port}`);
   });
   ```

3. Build the image:
   ```sh
   pack build my-node-app --builder paketobuildpacks/builder:base
   ```

4. Run the container:
   ```sh
   docker run -p 3000:3000 my-node-app
   ```

5. Access the application at `http://localhost:3000`

## CI/CD Integration
Cloud Native Buildpacks can be integrated into CI/CD pipelines. Example GitHub Actions workflow:

```yaml
name: CI Buildpack
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2
      - name: Install Pack CLI
        run: |
          curl -sSL "https://github.com/buildpacks/pack/releases/latest/download/pack-linux-amd64.tgz" | tar -xz -C /usr/local/bin
      - name: Build Image
        run: pack build my-app --builder paketobuildpacks/builder:base
      - name: Push to Docker Hub
        run: docker push my-dockerhub-username/my-app
```
