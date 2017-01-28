## Docker Contains for Rust
Installing Rust on VMs such as VirtualBox is good and works well. However, for quick builds for your Rust environment in a different OS than your default OS (i.e, OSX), the following are available:

rust-ubuntu

*Note: All of the rust images have openssl libs/packages so it's easy to build any app/lib that depends on OpenSSL.*

## Instructions
**Dependency - Docker for your environment**

These images exist on the DockerHub at `lambdastack` so, do the following to get up and running quickly:

```
docker run -it --rm -p 8000:8000 -v $(pwd):/source lambdastack/rust-ubuntu
```

*Note: The -p 8000:8000 is optional. Shown above to show how to map port 8000 in your host to port 8000 in the docker container. If your app does not accept TCP/IP connections like a web server then just ignore it.*

The `-v $(pwd):/source` is important. You will automatically be dropped into a `bash` shell in the given OS (i.e., Ubuntu) in the `/rust` directory. Simply `cd /source` to get to your development directory that's mapped to your host's drive.

*NB: IF your Cargo.toml file contains a `{ path = <whatever path> }` then you will need to launch the above command from the parent of both the app/lib you're building and the `path` you specified in your Cargo.toml file. You can also just pass in the parent folder instead of specifying `$(pwd)`.*

If your app was a web server (like klaus or nginx) then you could launch your browser and point it to `localhost:8000` if your app was running in the docker container.
