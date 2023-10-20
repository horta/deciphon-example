# Hello Sandy 👋

I will show the steps to run Deciphon server and populate it with some data
so that you can better test deciphon_web.

Assuming you have Docker installed, you can enter

```sh
docker compose --env-file compose.cfg up
```

to start it. Check out [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) for
the API documentation.

You probably won't need any custom configuration.
But if you think you do, check out `compose.cfg` for information.

You can use `deciphonctl` to populate it with protein database and to perform scans.

You can install it via

```sh
pipx install deciphonctl
```

(Or via `pip` if you prefer it.)

You will need to direct deciphonctl to the server:

```sh
export DECIPHONCTL_SCHED_URL=http://127.0.0.1:8000
export DECIPHONCTL_S3_URL=http://127.0.0.1:9000/deciphon
```

And now we can add a protein database and scan a sequence against it:

```sh
# Upload minifam.hmm for processing according to NCBI genetic code 11
deciphonctl hmm add minifam.hmm 11

# Check its processing state
deciphonctl hmm ls

# Once it is done, you should be able
# to see the protein database by entering
deciphonctl db ls

# Submit a sequence for scan against
# minifam database
deciphonctl scan add enzime.fna 1

# Check its state
deciphonctl scan ls

# Once it is done, visualize its result
deciphonctl scan snap-view 1
```
