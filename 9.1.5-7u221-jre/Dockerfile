FROM openjdk:7u221-jre

ENV JETTY_HOME /usr/local/jetty
ENV JETTY_BASE /var/lib/jetty
ENV TMPDIR /tmp/jetty
ENV PATH $JETTY_HOME/bin:$PATH
ENV JETTY_TGZ_URL https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.1.5.v20140505/jetty-distribution-9.1.5.v20140505.tar.gz


RUN set -xe \
&& mkdir -p "$JETTY_HOME" \
&& cd $JETTY_HOME \
&& curl -SL "$JETTY_TGZ_URL" -o jetty.tar.gz \
&& curl -SL "$JETTY_TGZ_URL.asc" -o jetty.tar.gz.asc \
&& tar -xvf jetty.tar.gz --strip-components=1 \
&& sed -i '/jetty-logging/d' etc/jetty.conf \
&& rm -fr jetty.tar.gz* \
&& mkdir -p "$JETTY_BASE" \
&& cd $JETTY_BASE \
&& java -jar "$JETTY_HOME/start.jar" --add-to-startd=http \
&& mkdir -p "$TMPDIR" \
&& groupadd -r jetty && useradd -r -g jetty jetty \
&& chown -R jetty:jetty "$JETTY_HOME" "$JETTY_BASE" "$TMPDIR"\
&& rm -rf /tmp/hsperfdata_root



USER jetty
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/local/jetty/start.jar"]