
# Lab 00 - Environment Setup

## Objective

Prepare a local AWS engineering environment using
Docker, Floci and AWS CLI.

## Architecture

- Docker Desktop: container runtime.
- Floci: local AWS API emulator.
- AWS CLI: AWS service interaction.
- GitHub: source control and documentation.

## Prerequisites

- Docker Engine / Docker Desktop
- Docker Compose v2
- AWS CLI v2
- Git

## Implementation

1. Start Floci using Docker Compose.
2. Configure dummy AWS credentials.
3. Connect AWS CLI to localhost:4566.
4. Create an S3 bucket.
5. Upload and list an object.
6. Remove the test resources.

## Validation

The following operations must succeed:

- [ ] Floci container is running.
- [ ] AWS CLI can reach Floci.
- [ ] S3 bucket creation succeeds.
- [ ] Object upload succeeds.
- [ ] Object listing succeeds.
- [ ] Resources are removed.

## Troubleshooting

Document errors, root causes and solutions here.

## Lessons Learned

Document the AWS concepts and technical
knowledge acquired during this lab.

## Cleanup

Remove test resources and stop Floci when
the laboratory is no longer needed.
