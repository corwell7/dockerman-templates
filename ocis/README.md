# INSTRUCTIONS
Adapted from the official docs: https://doc.owncloud.com/ocis/next/deployment/container/container-setup.html
1. Create the following directories (assuming your appdata is in /mnt/appdata/) beforehand using the unraid terminal:

```
mkdir /mnt/user/appdata/ocis
mkdir /mnt/user/appdata/ocis/ocis-config
mkdir /mnt/user/appdata/ocis/ocis-data
```

2. Change the owner of the new directories to the UID/GID required by the container:
```
chown -Rfv 1000:1000 /mnt/user/appdata/ocis/
```

3. Run the following (in the terminal) to initialise the config. \
   Make sure the source path is the same as the /ocis-config directory you just created. \
   Replace \<CURRENTVERSION> with the latest stable release (e.g. 5.0.2). Do not use the :latest tag. \
   You can find releases here: https://github.com/owncloud/ocis/releases.
```
docker run --rm -it \
    --mount type=bind,source=/mnt/user/appdata/ocis/ocis-config,target=/etc/ocis \
    owncloud/ocis:<CURRENTVERSION> init
```
4. You will see the following in the terminal:
```
Do you want to configure Infinite Scale with certificate checking disabled?
This is not recommended for public instances! [yes | no = default]
```
Type 'yes' and hit enter (unless you are providing a signed cert).

5. You will then see the following. These are the initial admin credentials you will use to login. The password should be changed upon logging in. 
```
=========================================
 generated OCIS Config
=========================================
 configpath : /etc/ocis/ocis.yaml
 user       : admin
 password   : <removed for documentation>
```
6. You can now create the container from the template. Read each envvar / path description carefully. 