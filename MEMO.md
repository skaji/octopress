## install

    git clone --recursive -o source git@github.com:shoichikaji/octopress.git
    cd octopress
    git clone git@github.com:shoichikaji/shoichikaji.github.io.git _deploy
    bundle install

## new post

    ./new_post title
    ./rake new_post\['title'\]

## preview

    ./rake preview

## generate && deploy

    ./rake generate
    ./rake deploy
