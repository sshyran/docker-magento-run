### Up magento without install php, nginx, mysql

1\. Run using docker:

`docker run -p 80:80 -p 443:443 -p 22:22 -v `pwd`/docker-runtime/logs/nginx:/var/log/nginx -v `pwd`/docker-runtime/data/mysql:/var/lib/mysql -v `pwd`:/var/www/html/web hws47a/magento-run -d`

or using docker-compose (copy it to your project)  

`docker-compose up -d`

2\. Create new db and import magento here (if needed)

`docker exec -i <container_name> mysqladmin create magento`  
`docker exec -i <container_name> mysql magento < dump.sql`

3\. Change app/etc/local.xml in \<connection> section to 

                    <host><![CDATA[127.0.0.1]]></host>
                    <username><![CDATA[]]></username>
                    <password><![CDATA[]]></password>
                    <dbname><![CDATA[magento]]></dbname>

4\. Open website by adding in browser 127.0.0.1, localhost or other host added to /etc/hosts 

5\. Add `docker-runtime` directory to .gitignore

#### Connect to container

You can connect to container using either `docker exec` or `ssh`:

* `docker exec -it <container> /bin/bash`
* `ssh root@0.0.0.0`

Ssh can be also used to connect to mysql using clients on host like SequelPro

#### Troubleshooting

1\. Disable default apache on macosx 

`sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist`
