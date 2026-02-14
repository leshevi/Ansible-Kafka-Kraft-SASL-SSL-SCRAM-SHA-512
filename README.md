Playbook create-key.yml to create a key and certificate, you can run it separately or as you wish. The simplest job for creating
```yml
stages:
  - 🚀deploy_cert

🚀ansible_job:
  stage: 🚀deploy_cert
  image: alpine:latest
  tags:
    - Docker
  before_script:
    - mkdir -p $CERT
    - apk add --no-cache ansible openssl
  script:
    - ansible-playbook create-key.yml -i "localhost," -c local
  artifacts:
    paths:
      - $CERT
    expire_in: 1 week
```
Then we take the artifacts and add them to Gitlab-ci variables as files and use the rest of the code to create a Kafka cluster.
