# We pull our base image from DockerHub
# We;d be using the slim version of Python's
# release allowing for a light-weight, secure
# version of Python for development.
#
# See also: https://medium.com/swlh/alpine-slim-stretch-buster-jessie-bullseye-bookworm-what-are-the-differences-in-docker-62171ed4531d
#
# I won't be going into Multi-builds configuration
# in this starter template. However, for a production-grade
# project, I highly recommend Multi-stage build with two layers
# of your images, one for development and the main build for prodction
#
# For Example,
#
#
# ```
# FROM python:3.9-buster AS dev
# ...
#
# FROM dev    OR    FROM newBaseImageForProduction
# ...               COPY --from=builder ...
# ENTRYPOINT
#
#
# ```
#
# See also: https://docs.docker.com/build/building/multi-stage/
# 
FROM python:3.10.slim-bullseye

# Set your 'docker' project-level environment variables
# Here, since this template is inclined towards Django projects
# We should tell Python to stick to some common rules such
# ignoring PyCache, Optionally, we could ignore PIP version check at
# stage builds and explicitly upgrade if we want to.
#
# CAUTION: Never hardcode senstive information in your docker or docker-compose files.
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV PIP_DISABLE_PIP_VERSION_CHECK 1

# Set your working directory as,
#   WORKDIR /the/workdir/path
WORKDIR /app

# Copy your requirements file into your build
COPY requirements/dev-requirements.txt .

# Install dependencies
# We should cache our dependencies in a production grade
# project, you could change the below line to
#
# ```
# RUN pip install 
# ```
# However, this is repository is targeted to complete beginners
# I would create an advanced starter template for Production Django
# projects later.
RUN pip install --no-cache-dir -r ./dev-requirements.txt

# Copy your source folder into your root build
# Careful here buddy,you don't want to accidentally
# increase build size with unneccessary files.
# Hence, the need for .dockerignore
# 
# The use of,
#
# ```
# COPY . .
# ```
# does not follow best practices. However, for the
# sake of starters, we would keep it at this.
COPY . .