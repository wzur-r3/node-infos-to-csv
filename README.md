# Network Map's Node information to CSV converter 

A simple filter to convert the nodes on the network map to a CSV file

## Table of Contents

- [Before you start](#before-you-start)
- [TL;DR](#tldr)
- [What does it do](#what-does-it-do)
- [References](#references)

_(TOC generated by [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

Before you start
----------------

This project requires [jq] for JSON parsing. See [jq]'s installation instructions, the link is in the
[References](#references) section.

Please have it installed first.

TL;DR
-----

To convert a JSON file with the node information produced by the Network Map, run the
[node-infos-to-csv](./node-infos-to-csv) script 

```bash
./node-infos-to-csv path-to-the-node-infos.json
```

What does it do
---------------

This script reads a JSON file with node information, as produced by the Network Map, and converts it to a comma
separated values (CSV) file. It reads that file either from its input, thus making it suitable to use as a filter,
or reads the content from its first parameter.

So:

```bash
./node-infos-to-csv path-to-the-node-infos.json
```

and 

```bash
cat path-to-the-node-infos.json | ./node-infos-to-csv
```

would work the same. Specifically, it will work with a tool like `curl`, for example:

```bash
curl -q https://[compatibilityZoneURL]/network-map/json/node-infos | ./node-infos-to-csv >node-infos.csv
```

see http://docs.netman.r3.com/releases/head/network-map-overview.html?highlight=json#http-network-map-protocol

To adapt the data format used by the Network Map, the following changes are made:

* `Legal Indentities` array is flatten into a string, and entries are merged with a semicolon (`;`)
* `Addresses` array is flatten into a string as follows:
    * `host` and `port` are merged with a double colon (`:`)
    * `host:port` are merged with a comma (`,`)
 

References
----------

* [jq] - see the [official documentation](https://stedolan.github.io/jq/manual/) and the [installation instructions](https://stedolan.github.io/jq/download/)

[jq]: https://stedolan.github.io/jq "jq is a lightweight and flexible command-line JSON processor."
