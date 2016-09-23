# How to point a newly created Fedora+GSearch at existing Fedora data

This assumes that the Fedora version does not change. 

## Stop Tomcat

Stop tomcat. It can't be running when you do this. 

## Edit the Fedora Skubra Storage properties


Edit `$FEDORA_HOME/server/config/spring/akubra-llstore.xml` to set the path for fsDatastreamStore and fsObjectStore to the location of the existing data. 

```
  <bean name="fsObjectStore" class="org.akubraproject.fs.FSBlobStore"
      singleton="true">
      <constructor-arg value="urn:example.org:fsObjectStore" />
 -    <constructor-arg value="/usr/local/fedora/data/objectStore"/>
 +    <constructor-arg value="/mnt/islandoradata1/prod/fedora-data/objectStore"/>
  </bean>
```

```
  <bean name="fsDatastreamStore" class="org.akubraproject.fs.FSBlobStore"
       singleton="true">
      <constructor-arg value="urn:example.org:fsDatastreamStore" />
  -   <constructor-arg value="/usr/local/fedora/data/datastreamStore"/>
  +   <constructor-arg value="/mnt/islandoradata1/prod/fedora-data/datastreamStore"/>
  </bean>
```

## Rebuild the Fedora Resource Index and SQL Database

Run fedora-rebuild.sh  

```
sudo -E -u tomcat $FEDORA_HOME/server/bin/fedora-rebuild.sh
# -E to preserve environment variables, like $FEDORA_HOME
```

Choose option 1 to rebuild the Resource Index. Then re-run `fedora-rebuild.sh` and choose option 2 to rebuild the SQL database.

## Point GSearch at the Fedora object store


Edit `$CATALINA_HOME/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/repository/FgsRepos/repository.properties`

```
  - fgsrepository.fedoraObjectDir    = /usr/local/fedora/data/objectStore
  + fgsrepository.fedoraObjectDir    = /mnt/islandoradata1/prod/fedora-data/objectStore
```


## Restart Tomcat

At this point you should be able to see your content in Islandora, but it will not be searchable. 

## Build a new Solr Index

Create a new empty Solr index. This should happen fast. 

```
curl -u fgsAdmin:gsearchPassword -X GET "http://localhost:8080/fedoragsearch/rest?operation=updateIndex&action=createEmpty"
```

Index the contents of Fedora into Solr. This will take awhile. 

```
curl -u fgsAdmin:gsearchPassword -X GET "http://localhost:8080/fedoragsearch/rest?operation=updateIndex&action=fromFoxmlFiles"
```

