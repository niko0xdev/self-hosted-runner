# Self-Hosted Runner for GitHub Actions with Docker

This project provides a self-hosted runner for GitHub Actions with Docker support. It allows you to run your GitHub Actions workflows on different operating systems using Docker containers. The supported operating systems include Ubuntu 20.04, CentOS 7, and Alpine 3.5.

## Prerequisites

To use this self-hosted runner, you need to have the following prerequisites installed:

- Docker: Make sure you have Docker installed on your machine. You can download and install Docker from the official website: [https://www.docker.com/](https://www.docker.com/)

## Setup Instructions

Follow these steps to set up the self-hosted runner with Docker:

1. Clone the repository:

   ```bash
   git clone https://github.com/niko0xdev/self-hosted-runner.git
   cd self-hosted-runner
   ```

2. Build the Docker image for the runner. Replace `ubuntu/20.04` with `centos/7` or `alpine/3.5` depending on the operating system you want to use:

   ```bash
   docker build -t self-hosted-runner:ubuntu-20.04 -f Dockerfile.ubuntu-20.04 .
   ```

   or

   ```bash
   docker build -t self-hosted-runner:centos-7 -f Dockerfile.centos-7 .
   ```

   or

   ```bash
   docker build -t self-hosted-runner:alpine-3.5 -f Dockerfile.alpine-3.5 .
   ```

3. Configure the runner:

   - Open the `config.sh` file and set the following variables:

     - `GITHUB_REPOSITORY`: Your GitHub repository in the format `owner/repo`.
     - `RUNNER_NAME`: The name of your runner.
     - `GITHUB_RUNNER_TOKEN`: Your GitHub Personal Access Token with the `repo` scope. You can create a token from your GitHub account settings.

4. Start the runner:

   ```bash
   docker run -d --name self-hosted-runner -e REPO_URL=https://github.com/yourusername/yourrepository -e REPO_TOKEN=YOUR_TOKEN self-hosted-runner:ubuntu-20.04
   ```

   Replace `self-hosted-runner:ubuntu-20.04` with the appropriate image tag for the operating system you want to use.

   Note: Make sure to replace `https://github.com/yourusername/yourrepository` with the URL of your GitHub repository and `YOUR_TOKEN` with your GitHub Personal Access Token.

5. Verify that the runner is connected:

   - Go to your GitHub repository.
   - Navigate to **Settings** -> **Actions** -> **Runners**.
   - You should see your self-hosted runner listed there.

## Usage

Once the self-hosted runner is set up and connected to your repository, you can start using it in your GitHub Actions workflows. Configure your workflows to use the self-hosted runner by specifying the `runs-on` parameter in your workflow file.

Example:

```yaml
jobs:
  build:
    runs-on: self-hosted
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      # Add your workflow steps here
```

The `runs-on: self-hosted` parameter instructs GitHub Actions to use a self-hosted runner for this job.

## Contributing

Contributions are welcome! If you have any ideas, improvements, or bug fixes, please open an issue or submit a pull request on the GitHub repository.

## License

This project is licensed under the [MIT License](LICENSE).
