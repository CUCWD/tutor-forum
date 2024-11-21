# Because the version of Debian `Slim` is LTS not supported we
# need to build from this previous image.

# Because we have not extended the `cs_comments_service` ruby application and
# only modified the MongoDB Atlas replica set connection string information
# there is no need to fork this repo and pull in our own version.
FROM overhangio/openedx-forum:13.0.0

USER app

# Override the MongoDB connection (replica set)
COPY --chown=app:app ./mongoid.yml /app/cs_comments_service/config/mongoid.yml

ENTRYPOINT ["docker-entrypoint.sh"]

ENV SINATRA_ENV staging
ENV NEW_RELIC_ENABLE false
ENV API_KEY forumapikey
ENV SEARCH_SERVER "http://elasticsearch:9200"
ENV MONGODB_AUTH ""
ENV MONGOID_AUTH_MECH ""
ENV MONGODB_HOST "mongodb"
ENV MONGODB_PORT "27017"
ENV MONGODB_DATABASE "cs_comments_service"
EXPOSE 4567
CMD ./bin/unicorn -c config/unicorn_tcp.rb -I '.'
