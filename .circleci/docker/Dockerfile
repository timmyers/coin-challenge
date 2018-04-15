FROM circleci/python:2.7

USER root

RUN pip install ansible
RUN pip install boto
RUN pip install docker-compose==1.15.0 

USER circleci

# FROM python:2.7.14-stretch

# RUN \
#   apt-get update && \
#     apt-get install \
#     apt-transport-https \
#     ca-certificates \
#     curl \
#     gnupg2 \
#     software-properties-common && \
#   curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
#   add-apt-repository \
#     "deb [arch=amd64] https://download.docker.com/linux/debian \
#     $(lsb_release -cs) \
#     stable" && \
#   apt-get update && \
#   apt-get install docker-ce

# RUN pip install ansible
# RUN pip install boto
# RUN pip install docker-compose