- # Monitor Application Logs
- Inspect Docker image in container is: `docker logs -f 8c3a101b556a` # image ref / or name
- Inspect k8s pod container image : `kubernetes logs -f webapp-02` # webapps02 is pod name
- Inspect k8s pod container image : `kubernetes logs -f webapp-02 simple-webapp` # webapps02 is pod name; where simple-webapp OR db are to be chosen to inspect the logs ==defaulted container "simple-webapp" out of: simple-webapp, db==
-
# Application Command
- From docker  `docker run ubuntu sleep 5`  # NoteOR creat a dockerfile FROM ubuntu CMD sleep CMD 5 OR ["sleep", "5]"
- OR FROM ubuntu ENTRYPOINT 10   # becomes docker run ubuntu-sleeper 10
- OR FROM ubuntu ENTRYPOINT ["sleep"] CMD ["5"] # defaults if parameter of 10 **or** is forgotten
- OR ENTRYPOINT can be overridden by a second instance of ENTRYPOINT ["sleep2.0"]
- ```cmake
  # docker example
  docker run --name ubuntu-sleeper \
  	--entrypoint sleep2.0
      ubuntu-sleeper 10
  ```
-