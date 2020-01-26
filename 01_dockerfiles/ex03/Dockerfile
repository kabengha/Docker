FROM ubuntu
RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install -y wget openssh-server ca-certificates
	RUN DEBIAN_FRONTEND=noninteractive apt-get install -y postfix tzdata
	RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && chmod 777 script.deb.sh && ./script.deb.sh
	RUN apt-get install gitlab-ce
	RUN echo "nginx['redirect_http_to_https'] = true \n nginx['redirect_http_to_https_port'] = true" >/etc/gitlab/gitlab.rb && \
	    echo "external_url 'https://192.168.99.100:443//'" > /etc/gitlab/gitlab.rb && \
		echo "gitlab_rails['gitlab_shell_ssh_port'] = 2222" >> /etc/gitlab/gitlab.rb && \
	    echo "nginx['redirect_http_to_https_port'] = 80\nnginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb && \
	    echo "Port 2222" >> /etc/ssh/sshd_config
WORKDIR /
RUN echo "service ssh restart" >> script.sh && \
	echo "(/opt/gitlab/embedded/bin/runsvdir-start&) && gitlab-ctl reconfigure" >> script.sh && \
	echo "tail -f /dev/null" >> script.sh
EXPOSE 443 80 2222
CMD ["sh","script.sh"]
# docker build -t ex03 .
# docker run -it -p 80:80 -p 2222:2222 -p 443:443 --privileged ex03 
