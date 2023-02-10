docker build --build-arg user=$(id -un) --build-arg group=$(id -gn) --build-arg uid=$(id -u) --build-arg gid=$(id -g) --no-cache -t atl_1350_image .
docker run -ti -d --name alt_1350 -v /home/$(id -u)/.ssh:/home/$(id -u)/.ssh -v /home/$(id -u)/workspace:/home/$(id -u)/workspace atl_1350_image /bin/bash
