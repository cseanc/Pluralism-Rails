# foreman

Run puma server and webpack-dev-server in one command.

## Install foreman

```bash
gem install foreman
```

## Create Procfile

At project root, create a file named `Procfile.dev` with this content:

```bash
web: bundle exec puma -C config/puma.rb
webpacker: ./bin/webpack-dev-server
```

## Run

```bash
foreman start -f Procfile.dev
```

## Alias

Since this command is long, you can set an alias in `~/.bash_profile` as shortcut:

```bash
# Add this line into ~/.bash_profile
alias fs="foreman start -f Procfile.dev"

# Save and run
source ~/.bash_profile

# At project root, you can run foreman by typing:
fs
```
