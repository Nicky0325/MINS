FROM ros:noetic-perception-focal

ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=1000

ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO=noetic

RUN apt-get update \
    && apt-get install --no-install-recommends --yes \
        build-essential \
        ca-certificates \
        git \
        python3-catkin-tools \
        sudo \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --gid "${USER_GID}" "${USERNAME}" \
    && useradd --uid "${USER_UID}" --gid "${USER_GID}" --create-home --shell /bin/bash "${USERNAME}" \
    && usermod --append --groups sudo "${USERNAME}" \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > "/etc/sudoers.d/${USERNAME}" \
    && chmod 0440 "/etc/sudoers.d/${USERNAME}"

RUN echo "source /opt/ros/noetic/setup.bash" >> "/home/${USERNAME}/.bashrc"

RUN mkdir -p /workspaces/src \
    && chown -R "${USERNAME}:${USERNAME}" /workspaces

WORKDIR /workspaces
USER ${USERNAME}
