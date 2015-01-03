# ncbi-blast-docker

[NCBI BLAST](http://blast.ncbi.nlm.nih.gov/) binaries in a Docker image, particularly for use with the [Galaxy
platform](http://galaxyproject.org/).

## Available Tags/Versions
The `simonalpha/ncbi-blast-docker` repository provides Dockerfiles for a number of BLAST versions, these are set up as [automated builds](https://reqistry.hub.docker.com/u/simonalpha/ncbi-blast-docker) on the public
[Docker Hub Registry](https://registry.hub.docker.com).

The available tags are:

- latest (default): NCBI BLAST+ 2.2.30+ (aliased to 2.2.30plus)
- 2.2.30plus: NCBI BLAST+ 2.2.30+
- 2.2.29plus: NCBI BLAST+ 2.2.29+
- 2.2.28plus: NCBI BLAST+ 2.2.28+
- 2.2.27plus: NCBI BLAST+ 2.2.27+
- 2.2.26plus: NCBI BLAST+ 2.2.26+

## Installation and Use

### Galaxy
Installation and use of a tool wrapper (links to follow) specifying one of these images will automatically pull and run (assuming that Galaxy's job_conf.xml has been [set up to use Docker](https://wiki.galaxyproject.org/Admin/Tools/Docker), and Docker is installed)

### General Use
1. Download an [automated build](https://registry.hub.docker.com/u/simonalpha/ncbi-blast-docker/) from public [Docker Hub Registry](https://registry.hub.docker.com/):

   `docker pull simonalpha/ncbi-blast-docker`

   Specific versions can be specified via tagging, for instance:

   `docker pull simonalpha/ncbi-blast-docker:2.2.30plus`

2. Run an instance of the image, mounting in directories with the required sequences/databases/files and setting the working directory as appropriate. If no program is specified, the default behaviour is to drop you into a shell in your working directory.

   `docker run --rm -v /home/simonalpha/project:/blast -v /databases:/db -w /blast simonalpha/ncbi-blast-docker`

   All the BLAST binaries in the default distribution are available and on the path, and you can run BLAST as usual.

   Another option is to provide a BLAST invocation when starting a container; much more useful for scripting! Ensure your BLAST invocation uses the paths you are mounting to in the container.

   `docker run --rm -v /home/simonalpha/project:/blast -v /databases:/db -w /blast simonalpha/ncbi-blast-docker blastp -query /blast/q_seq.faa -db /db/prot_db -out q_seq_V_prot_db`

The above is based strongly on how Galaxy uses Docker containers, however other methods are definitely possible. If you come across any, please do let us know.

I recommend use of `--rm` in your run commands, it automatically clears the containers after use. However, this requires you write your data into a mounted path, otherwise your results will be deleted with the container.

## Users and Permissions
These images currently run as root, to allow easy read-write access to mounted volumes. This will change in the future with enabling patches in Galaxy, based around UIDs rather than users.

## Repository Structure
The layout of this repository is based on the structure of the [Java Dockerfile](https://github.com/dockerfile/java) repository for clear separation of versions and easy setup of automated builds. Suggestions or Pull Requests for better organisation most welcome.
