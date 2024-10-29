# Qiime2-using-Docker
docker images | grep 'qiime'
# create container named qiime2_jr
docker run --name qiime2_jr -dit -v /home:/home -v /data:/data --user $(id -u jianlanr):$(id -g jianlanr) 830b60993ea9 bash
# list containers
docker container ls
# running container 
docker exec -it qiime2_jr bash
# stop container
docker container stop <container id>
# remove container
docker container rm <container id>
# go to directory
cd /home/jianlanr/Saliva_16srna
# srun script
srun docker exec -i <docker-container-name> bash < <path-to-qiime-script>
