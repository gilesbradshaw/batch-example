# Container image that runs your code
FROM gitea/tea as build

FROM ubuntu:latest
COPY --from=build /tea /tea
VOLUME [ "/app" ]
ENV HOME="/app"
ENTRYPOINT ["/tea"]
