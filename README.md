# docker-duplicity

linux container based on alpine linux that provide [__duplicity__](http://duplicity.nongnu.org/)

The following backend have been tested successfully:

 - ftp
 - ssh
 - hubic
 - backblaze

If a backend doesn't work because of a missing dependency, fell free to open an [issue](https://github.com/Speedy37/docker-duplicity/issues).

## How to use

This image is available on

 - docker hub:
   https://hub.docker.com/r/speedy37/duplicity/  
   `docker pull quay.io/speedy37/duplicity`
 - quay.io: 
   https://quay.io/repository/speedy37/duplicity  
   `docker pull speedy37/duplicity`

## Backblaze

Because I'm using backblaze nowadays and that duplicity backblaze backend is buggy, I did a full rewrite of the backend using backblaze official python library (b2). Until this is merged into master, I'll keep replacing the master implementation with the one provided here.

## Docker compose example

```yml
backup.X:
  image: speedy37/duplicity:alpine
  hostname: backup.X
  environment:
   PASSPHRASE: Passw@rd
  volumes:
   - /what/i/want/to/backup:/data
  command: duplicity
   --full-if-older-than 1M
   --asynchronous-upload
   /data
   target_url
```

If you want to cache metadata, add a volume for: `/root/.cache/duplicity`
