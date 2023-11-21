docker build --build-arg user=$(id -un) --build-arg group=$(id -gn) --build-arg uid=$(id -u) --build-arg gid=$(id -g) --no-cache -t alt_1350_image .
docker run -ti -d --name alt_1350 -v /home/$(id -gn)/.ssh:/home/$(id -gn)/.ssh -v /home/$(id -gn)/workspace:/home/$(id -gn)/workspace alt_1350_image /bin/bash
