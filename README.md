# docker-electrum-bitcoind
Run a Bitcoin Core ElectrumX server with one command.

A Docker configuration for running a full Bitcoin Core node behind an ElectrumX server.

## Usage

```
docker-compose up
```

This will pull the latest version of bitcoind and ElectrumX, start syncing the blockchain, generate an SSL certificate and start listening for secure Electrum traffic on port 55002.

All blockchain data will be stored in `./data/bitcoind` and all ElectrumX data will be stored in `./data/electrumx`. This
 is stored on the host machine and mounted in the docker container as a volume, meaning it will persist across reboots/up
dates/containers etc.

If there's an SSL certificate/key (`electrumx.crt`/`electrumx.key`) in `./data/electrumx`, it'll be used instead of generating a new one.

Once everything is synced (this can take a while) start your locally installed Electrum Bitcoin Wallet:

```
python3 run_electrum -1 -s [IP of your server]:55002:s
```

### I don't trust your images, how do I build them myself?

You can build `kylemanna/docker-bitcoind` and `lukechilds/electrumx` yourself here:

- https://github.com/kylemanna/docker-bitcoind
- https://github.com/lukechilds/docker-electrumx

