Container Scanning tools
-----------------
grype (OS and 3rd party library CVEs)
-----------------
```
mkdir grype

cat <<EOF > grype/Dockerfile
FROM alpine
USER root
RUN apk --no-cache add curl && curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin
ENTRYPOINT ["/usr/local/bin/grype"]
EOF

docker build grype -t grype
docker pull nginx
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock grype nginx
```
-----------------
syft (Software Bill of Materials - list of packages and 3rd party libraries install on container)
-----------------

mkdir syft

cat <<EOF > syft/Dockerfile
FROM alpine
USER root
RUN apk --no-cache add curl && curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin
ENTRYPOINT ["/usr/local/bin/syft"]
EOF

docker build syft -t syft
docker pull nginx
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock syft nginx

-----------------
trivy (OS and 3rd party library CVEs)
-----------------
```
docker pull nginx
docker run aquasec/trivy image nginx
