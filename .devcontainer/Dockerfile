FROM python:3.14

RUN apt-get update

WORKDIR /usr/src/11ty

# Install Python dependencies
COPY .devcontainer/requirements.txt .devcontainer/requirements.txt
RUN python -m pip install --upgrade pip
RUN pip install --no-cache-dir -r .devcontainer/requirements.txt

COPY package*.json ./
COPY mise.toml ./
COPY .node-version ./

RUN curl https://mise.run | sh

# this collides with the .bashrc file john loads on the fly via VS Code settings
# TODO: if we can figure out another way to do this that subsequent RUN commands will honor
# we could just call 'mise trust', 'npm ci ' and 'npm start'
# (presumably) each call to RUN spawns a brand new terminal session
RUN echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc

 # mise trust
RUN ~/.local/bin/mise trust
# npm install
RUN ~/.local/bin/mise exec node -- npm ci

COPY . .

# npm start
ENTRYPOINT ~/.local/bin/mise exec node -- npm start

