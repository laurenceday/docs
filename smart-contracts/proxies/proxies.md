# [@indexed-finance/proxies](https://github.com/indexed-finance/proxies)

[Github](https://github.com/indexed-finance/proxies)

[NPM](https://www.npmjs.com/package/@indexed-finance/proxies)

Indexed uses proxies to instantiate many clones of specific contract templates. Index pools and their initialization contracts are deployed as proxies, which greatly reduces gas costs and allows any discovered bugs to be patched without any migration procedure.

A Proxy Manager contract controls the deployment and upgrading of proxies and their implementations. The proxy manager is controlled by the governance contract, which can add new contract templates that proxies can use, deploy singleton proxies, modify the implementation addresses of existing proxies, and approve specific addresses to deploy copies of an existing template.

The manager can deploy two types of proxies: many-to-one and one-to-one.

A one-to-one proxy is a single proxy contract which stores its own implementation address. When the proxy is called, it reads the implementation address from storage and delegates the transaction to it.

A many-to-one proxy is a proxy contract which shares an implementation address with many other proxies. Implementations for many-to-one proxies are identified by a 32 byte ID which is mapped to an implementation holder contract. The implementation holder's address is stored in the proxy contracts' bytecode as a constant value. When the proxy is called, it queries the implementation address from the implementation holder, then delegates the transaction to it.