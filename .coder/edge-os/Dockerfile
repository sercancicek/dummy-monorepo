# Stage: bring in Python 3.11
FROM python:3.11-slim-bookworm AS py311

# Final image with both 3.11 and 3.12
FROM python:3.12-slim-bookworm

ARG NEXUS_USERNAME
ARG NEXUS_PASSWORD
ARG PROJECT_PATH

# add Python 3.11 side-by-side
COPY --from=py311 /usr/local/bin/python3.11 /usr/local/bin/
COPY --from=py311 /usr/local/bin/pip3.11 /usr/local/bin/
COPY --from=py311 /usr/local/include/python3.11 /usr/local/include/python3.11
COPY --from=py311 /usr/local/lib/python3.11 /usr/local/lib/python3.11
COPY --from=py311 /usr/local/lib/libpython3.11*.so* /usr/local/lib/

# Upgrade system, install utilities
RUN apt-get update \
  && apt-get upgrade -y --no-install-recommends \
  && apt-get install -y --no-install-recommends \
      curl jq net-tools openssh-client git procps sudo \
  && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN pip install --no-cache-dir --upgrade poetry==1.8.2

# Create picnic user
RUN groupadd --gid 1000 picnic \
    && useradd --create-home --uid 1000 --gid 1000 picnic \
    && echo picnic ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/picnic \
    && chmod 0440 /etc/sudoers.d/picnic

# Ensure picnic user can run docker
RUN groupadd docker \
    && adduser picnic docker

USER picnic

# Install Python dependencies
WORKDIR /home/picnic
COPY ${PROJECT_PATH}/pyproject.toml ${PROJECT_PATH}/poetry.lock ./
RUN poetry config -- http-basic.picnic ${NEXUS_USERNAME} ${NEXUS_PASSWORD}
RUN poetry install --sync

# Set workdir where project is mounted within the dev container
WORKDIR /workspaces/picnic-edge/${PROJECT_PATH}
