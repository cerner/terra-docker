# This dockerfile provides a docker image setup with zshell for developers to use as a common node development environment.
# This image copies no code in and can be used directly with a volume mount to add code to the /opt/module directory.
FROM cerner/terra-node-base:latest

# Open up port 9229 for node debugging
EXPOSE 9229

# Install zsh / oh-my-zsh
RUN apk add zsh curl wget \
  && wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true\
  # Setup history folder
  && mkdir /root/zsh_history\
  # Save history in a folder to allow for cacheing in a docker volume
  && sed -i 's+$HOME/.zsh_history+$HOME/zsh_history/.zsh_history+g' /root/.oh-my-zsh/lib/history.zsh\
  # Apply custom zsh theme to add to the prompt to identify this as a [dev] shell.
  && sed -i 's+ZSH_THEME="robbyrussell"+ZSH_THEME="terra-docker"+g' /root/.zshrc

# Add custom theme.
ADD ./themes /root/.oh-my-zsh/themes

# Do not end tests after the first failure.
ENV WDIO_BAIL false

# Run a custom command to start zsh. Check to see if a package env has been setup and cd to that directory before starting the shell.
CMD /bin/zsh
