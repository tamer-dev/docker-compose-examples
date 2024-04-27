# Description
Run Fresh Laravel App

### Quick Start

1. Run `Docker Compose` dependencies.
   
        docker compose up -d

2. go to Project folder.
   
        cd src

3. make new fresh laravel project.
   
        docker run --rm --interactive --tty --volume $PWD:/app composer create-project laravel/laravel .

    or git clone you project and run

        docker run --rm --interactive --tty --volume $PWD:/app composer install
       