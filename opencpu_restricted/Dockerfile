FROM polmine/opencpu_public

COPY opencpu.conf /etc/apache2/sites-available/opencpu.conf 

RUN mkdir /usr/local/apache && mkdir /usr/local/apache/passwd 
COPY passwords /usr/local/apache/passwd/passwords
