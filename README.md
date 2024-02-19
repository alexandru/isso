# Publish Isso

Update from upstream:

```
git remote add upstream https://github.com/posativ/isso.git
git fetch upstream
git merge upstream/master
```

Build and publish Docker image:

```
docker build . -t alexelcu/isso:latest
docker push alexelcu/isso:latest

export ISSO_VERSION="v$(date +"%Y-%m-%d")"
docker tag alexelcu/isso:latest "alexelcu/isso:$ISSO_VERSION"
docker push "alexelcu/isso:$ISSO_VERSION"
```

Link: <https://hub.docker.com/repository/docker/alexelcu/isso>
