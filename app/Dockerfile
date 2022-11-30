FROM alpine:latest
USER root

RUN apk update
RUN apk fetch openjdk8
RUN apk add openjdk8
ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
ENV PATH="$JAVA_HOME/bin:${PATH}"

RUN apk add --update net-tools
RUN apk add vim
RUN apk add --no-cache python3

RUN apk add --update --no-cache openssh
RUN mkdir -p /root/.ssh \
    && chmod 0700 /root/.ssh \
    && echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQD1DR6D2zjzeYB1/eGWhVuIs08K9v+v4E1anDCK3WsuqByssVTw9SSmPtyQA6Tjpw81I1QQptXILu6ZuvcQF5KJOCKoymrGWR8RAQcP/s9GGe6CNjcWY6lrmPrgItia4W+J3bUvJ5bt+RfQjnvfbuj34iF19Ua7bgSsEx4zVN2SkqUdV6P2IOlev+prdwpRyp6iYOjWVBUR7D7NCc/+1XteYfyokQYZ5j14HrPMH/EKGtR9gyENbkblpqJ2uxaXJDgGL774lia941z5jJbq+IPMsdDE1C7jRdPD9mGXAI1Gqj5K2Zbv/galwuQ+QQv62V+Or0AGEHUydTrzkonFixniga+hGn0xGnSd8kawXNO4OONyPpsOhdlAtbHFm4GaIkbZd1zT9cJaFVBrlvhP4JZYezwJGovXbaeuCoIgTmPsTMi6ujtZwUSEFw5+lTy3+cYlbPTCsV7EOnUBwr7UdEBk7G339wp6WTSAnADevB9Uc3ZFkBfvBnQGNXFjMZF54nc= jenkins@2122b5899ee2" > /root/.ssh/authorized_keys \
    && mkdir -p /run/openrc \
    && touch /run/openrc/softlevel

RUN echo 'PasswordAuthentication no' >> /etc/ssh/sshd_config
RUN java -version
ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 22
COPY entrypoint.sh /