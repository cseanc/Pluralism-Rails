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

