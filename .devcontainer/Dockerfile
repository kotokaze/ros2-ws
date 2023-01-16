FROM tiryoh/ros2-desktop-vnc:${templateOption:imageVariant}

# [Option] Install zsh
ARG INSTALL_ZSH="true"
# [Option] Upgrade OS packages to their latest versions
ARG UPGRADE_PACKAGES="false"

# [Optional] Uncomment to use mirror for apt
RUN sed -i 's\http://archive.ubuntu.com/ubuntu/\mirror://mirrors.ubuntu.com/mirrors.txt\' /etc/apt/sources.list;

# Install needed packages and setup non-root user. Use a separate RUN statement to add your
# own dependencies. A user of "automatic" attempts to reuse an user ID if one already exists.
ARG USERNAME=automatic
ARG USER_UID=1000
ARG USER_GID=$USER_UID
COPY library-scripts/*.sh /tmp/library-scripts/
RUN apt-get update \
  && /bin/bash /tmp/library-scripts/common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true" \
  # Clean up
  && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# [OPtional] Install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#   && apt-get -y install --no-install-recommends <your-package-list-here>
