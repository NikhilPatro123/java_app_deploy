Started by user Ch Nikhil Patro
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins in /var/lib/jenkins/workspace/deploy-1
[Pipeline] {
[Pipeline] stage
[Pipeline] { (code)
[Pipeline] git
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/lib/jenkins/workspace/deploy-1/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/NikhilPatro123/java_app_deploy.git # timeout=10
Fetching upstream changes from https://github.com/NikhilPatro123/java_app_deploy.git
 > git --version # timeout=10
 > git --version # 'git version 2.50.1'
 > git fetch --tags --force --progress -- https://github.com/NikhilPatro123/java_app_deploy.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
Checking out Revision 1ef7d8027a8314d9951107c1a716fd4b79c6b86e (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 1ef7d8027a8314d9951107c1a716fd4b79c6b86e # timeout=10
 > git branch -a -v --no-abbrev # timeout=10
 > git branch -D master # timeout=10
 > git checkout -b master 1ef7d8027a8314d9951107c1a716fd4b79c6b86e # timeout=10
Commit message: "Update pom.xml"
 > git rev-list --no-walk 1ef7d8027a8314d9951107c1a716fd4b79c6b86e # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (build)
[Pipeline] sh
+ mvn clean package
[INFO] Scanning for projects...
[INFO] 
[INFO] -------------------------< in.javahome:myweb >--------------------------
[INFO] Building Java Home myweb 8.7.8
[INFO] --------------------------------[ war ]---------------------------------
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ myweb ---
[INFO] Deleting /var/lib/jenkins/workspace/deploy-1/target
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myweb ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/deploy-1/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myweb ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ myweb ---
[WARNING] Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
[INFO] skip non existing resourceDirectory /var/lib/jenkins/workspace/deploy-1/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ myweb ---
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ myweb ---
[INFO] No tests to run.
[INFO] 
[INFO] --- maven-war-plugin:3.3.1:war (default-war) @ myweb ---
[INFO] Packaging webapp
[INFO] Assembling webapp [myweb] in [/var/lib/jenkins/workspace/deploy-1/target/myweb-8.7.8]
[INFO] Processing war project
[INFO] Copying webapp resources [/var/lib/jenkins/workspace/deploy-1/src/main/webapp]
[INFO] Building war: /var/lib/jenkins/workspace/deploy-1/target/myweb-8.7.8.war
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.422 s
[INFO] Finished at: 2025-08-15T12:18:31Z
[INFO] ------------------------------------------------------------------------
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (dockerimage)
[Pipeline] sh
+ docker build -t nikhilpatro05/dockeriamge .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 232B done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/tomcat:8.0.20-jre8
#2 DONE 1.3s

#3 [internal] load .dockerignore
#3 transferring context: 2B done
#3 DONE 0.0s

#4 [internal] load build context
#4 transferring context: 2.47kB done
#4 DONE 0.0s

#5 [1/3] FROM docker.io/library/tomcat:8.0.20-jre8@sha256:579e042fb31e6975062276489cbdb3d9c942661a1d489f122d29ce2249e2ed34
#5 resolve docker.io/library/tomcat:8.0.20-jre8@sha256:579e042fb31e6975062276489cbdb3d9c942661a1d489f122d29ce2249e2ed34
#5 resolve docker.io/library/tomcat:8.0.20-jre8@sha256:579e042fb31e6975062276489cbdb3d9c942661a1d489f122d29ce2249e2ed34 0.3s done
#5 DONE 0.3s

#6 [2/3] COPY tomcat-users.xml /usr/local/tomcat/conf/tomcat-users.xml
#6 CACHED

#7 [3/3] COPY target/*.war /usr/local/tomcat/webapps/myweb.war
#7 DONE 0.0s

#8 exporting to image
#8 exporting layers 0.0s done
#8 writing image sha256:93797b9c7326fd215009ddd751a8ca528d7c6d1bad339a5f5ea6e5f5e362546f done
#8 naming to docker.io/nikhilpatro05/dockeriamge done
#8 DONE 0.0s
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (imagepush)
[Pipeline] withDockerRegistry
$ docker login -u nikhilpatro05 -p ******** https://index.docker.io/v1/
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
WARNING! Your password will be stored unencrypted in /var/lib/jenkins/workspace/deploy-1@tmp/6b1f05b1-7626-45d1-be44-ebcb4eca2cbc/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
[Pipeline] {
[Pipeline] sh
+ docker push nikhilpatro05/dockeriamge
Using default tag: latest
The push refers to repository [docker.io/nikhilpatro05/dockeriamge]
246062b7d048: Preparing
74ca6ed0ba66: Preparing
3d7c7b65abb2: Preparing
c8252e277764: Preparing
0d059c7d8519: Preparing
0e413cd50c1e: Preparing
3770fb9237e7: Preparing
e3e44bf3000f: Preparing
fd97e4a10f39: Preparing
0e413cd50c1e: Waiting
3770fb9237e7: Waiting
e3e44bf3000f: Waiting
fd97e4a10f39: Waiting
c8252e277764: Layer already exists
3d7c7b65abb2: Layer already exists
0d059c7d8519: Layer already exists
74ca6ed0ba66: Layer already exists
0e413cd50c1e: Layer already exists
3770fb9237e7: Layer already exists
e3e44bf3000f: Layer already exists
fd97e4a10f39: Layer already exists
246062b7d048: Pushed
latest: digest: sha256:0c5afe128eb608b35d5694e7dbfaeb05da4f30cd4c497618d94d0351c958baef size: 2210
[Pipeline] }
[Pipeline] // withDockerRegistry
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (container)
[Pipeline] sh
+ docker run -itd --name cont1 -p 8082:8080 nikhilpatro05/dockeriamge
5775d449959cc9eade97ab25a84b577d0066d263bc7838a58e98d86c85a0b188
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
Finished: SUCCESS
