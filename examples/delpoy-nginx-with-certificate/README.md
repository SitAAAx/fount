# Example Nginx deployment with certificates

## Build container

Enter the _docker_ directory and execute:

```shell script
docker build --tag registry.k3s.l4b.space/fount-nginx-with-certificate-example:latest .
```

## Test container locally with Docker

```shell script
docker run -p 8080:80 --name example-nginx registry.k3s.l4b.space/fount-nginx-with-certificate-example:latest

```

## Push container to remote registry

```shell script
docker push registry.k3s.l4b.space/fount-nginx-with-certificate-example:latest
```

## Deploy example

```shell script
ansible-playbook example-deploy-nginx-with-certificate.yml
```
