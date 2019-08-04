FROM ubuntu:16.04

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
ca-certificates \
curl \
unzip \
jq \
git \
iputils-ping \
libcurl3 \
libicu55 \
libunwind8 \
python3-pip \
build-essential \
netcat \
libssl-dev \
python3-setuptools \
libffi-dev \
python3-dev \
&& pip3 install ansible==2.7.8 \
&& curl https://releases.hashicorp.com/terraform/0.12.6/terraform_0.12.6_linux_amd64.zip -o /bin/terraform.zip \
&& unzip /bin/terraform.zip -d /bin

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]
