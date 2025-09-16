FROM pgbouncer/pgbouncer:latest

USER root

# Install envsubst for template substitution
RUN apt-get update && apt-get install -y gettext-base && rm -rf /var/lib/apt/lists/*

# Copy configuration files
COPY pgbouncer.ini.template /etc/pgbouncer/pgbouncer.ini.template
COPY userlist.txt /etc/pgbouncer/userlist.txt

# Create entrypoint script
RUN echo '#!/bin/bash\n\
envsubst < /etc/pgbouncer/pgbouncer.ini.template > /etc/pgbouncer/pgbouncer.ini\n\
exec pgbouncer /etc/pgbouncer/pgbouncer.ini' > /entrypoint.sh && \
    chmod +x /entrypoint.sh

USER pgbouncer

EXPOSE 6432

ENTRYPOINT ["/entrypoint.sh"]
