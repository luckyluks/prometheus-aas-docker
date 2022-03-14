FROM prom/prometheus
# set up config folder structure
WORKDIR /etc/prometheus
RUN mkdir -p config/prometheus/targets
RUN mkdir -p config/prometheus/rules
# add config files
ADD rules.yml /etc/prometheus/config/prometheus/rules
ADD prometheus.yml /etc/prometheus/config/prometheus
ADD targets.yml /etc/prometheus/config/prometheus/targets

