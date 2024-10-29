# Qiime2-using-Docker
This project is aiming to use [Qiime2](https://qiime2.org/) through docker on either single-end or paired-end 16s processing.
### download data
    while IFS=, read -r col1; do echo "prefetch $col1"; done < SraAccList.csv > prefetch.sh
    while IFS=, read -r col1; do echo "fasterq-dump $col1"; done < SraAccList.csv > fastq-dump.sh
    chmod prefetch.sh / fastq-dump.sh
### work in a attached screen
    screen -S prefetch
    ctrl-a+d
    screen -r
### using sratoolkit
    export /home/jianlanr/sratoolkit.3.1.1-centos_linux64/bin
    ./prefetch.sh
    ./fastq-dump.sh
### docker images find Qiime2    
    docker images | grep 'qiime'
### create container named qiime2_jr
    docker run --name qiime2_jr -dit -v /home:/home -v /data:/data --user $(id -u jianlanr):$(id -g jianlanr) 830b60993ea9 bash
### list containers
    docker container ls
### running container 
    docker exec -it qiime2_jr bash
### stop container
    docker container stop <container id>
### remove container
    docker container rm <container id>
### go to directory
    cd /home/jianlanr/Saliva_16srna
### srun script
    srun docker exec -i <docker-container-name> bash < <path-to-qiime-script>
