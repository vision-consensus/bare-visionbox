# VisionBox bare-box

This is a bare-minimum VisionBox (https://github.com/vision-consensus/visionbox.git)  project (`visionbox init`)

## How to init a minimalistic VisionBox project

### Install VisionBox

If you don't have Node.js on your Mac/Linux computer, install it using preferably NVM. On Linux/Mac you can run:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

after open a new terminal and install the version of Node you prefer, for example the stable v10:

```
nvm install lts/dubnium
```

On Windows, you can install Nvm following the instructions at
https://github.com/coreybutler/nvm-windows



Once the npm is ready, install VisionBox globally

```
npm i -g visionbox
```

Then, create a directory and initialize bare-box project there
```
mkdir visionbox-example
cd visionbox-example
visionbox init
```

### Configure Network Information for VisionBox

To use VisionBox, your dApp has to have a network configuration file `visionbox.js` in the source root. This special file tells VisionBox how to connect to nodes, event server, and passes some special parameters, like the default private key.  

If you are connecting to **different** hosts for fullnode, solidity node, and event server, you may set `fullNode`, `solidityNode` and `eventServer` respectively:

```
module.exports = {
  networks: {
    development: {
			...
      fullNode: "http://127.0.0.1:8090",
      solidityNode: "http://127.0.0.1:8091",
      eventServer: "http://127.0.0.1:8080",
      network_id: "*"
    },
    mainnet: {
			...
      fullNode: "https://vtest.infragrid.v.network",
      solidityNode: "https://vtest.infragrid.v.network",
      eventServer: "https://vtest.infragrid.v.network",
      network_id: "*"
    }
  }
};
```

If you are connecting to the **same** host for fullnode, solidity node, and event server, you can just set `fullHost`:

```
module.exports = {
  networks: {
    development: {
			...
      fullHost: "http://127.0.0.1:8090",
      network_id: "*"
    },
    mainnet: {
			...
      fullHost: "https://vtest.infragrid.v.network",
      network_id: "*"
    }
  }
};
```

### Run the example dApp on local private network

`visionbox migrate` by default will use the `development` network. In order to test the smart contracts and deploy them locally, you must deploy a local fullnode with [vision-core](https://github.com/vision-consensus/vision-core).

**vision-core** (https://github.com/vision-consensus/vision-core)

Having the local fullnode ready, you may:

1. Setup the dApp.

```
visionbox migrate --reset
```

This command will invoke all migration scripts within the migrations directory.

2. Run the dApp:

```
npm run dev
```

It will automatically open the dApp in the default browser.