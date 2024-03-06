# Use the official Foundry image
FROM ghcr.io/foundry-rs/foundry:latest AS foundry

# Use an official Node.js base image
FROM node:20

# Copy Foundry binaries from the Foundry image
COPY --from=foundry /usr/local/bin/forge /usr/local/bin/forge
COPY --from=foundry /usr/local/bin/cast /usr/local/bin/cast
COPY --from=foundry /usr/local/bin/anvil /usr/local/bin/anvil

# Set the working directory in the container
WORKDIR /app
