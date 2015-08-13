FROM bmcustodio/archlinux-yaourt

MAINTAINER Matthew Eichler <matthew.eichler@aventinesolutions.nl>

RUN pacman --noconfirm -Suyy && pacman --noconfirm -S zsh

ADD sudoers /etc/sudoers

ENV APP_HOME /opt/rubie
RUN useradd --home-dir $APP_HOME --shell /bin/zsh --user-group --groups users,wheel rubie
ADD .zshrc $APP_HOME/.zshrc
ADD install_bootstrap_gems.sh $APP_HOME/install_bootstrap_gems.sh
RUN chown -Rv rubie $APP_HOME

# Set up  user + directory
USER rubie
WORKDIR $APP_HOME

# RVM for Rubies and Gems
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys '409B6B1796C275462A1703113804BB82D39DC0E3' && \
    curl -sSL https://get.rvm.io | bash -s stable --ruby=2.2.2

ENV PATH $PATH:$APP_HOME/.rvm/bin

RUN $APP_HOME/install_bootstrap_gems.sh && sudo pacman --noconfirm -S emacs-nox

CMD ["/bin/zsh"]
