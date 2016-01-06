# Running Openchain

Openchain is an open source distributed ledger technology. It is suited for organizations wishing to issue and manage digital assets in a robust, secure and scalable way. Visit [openchain.org](https://www.openchain.org/) for more information.

The full documentation for Openchain is available at [docs.openchain.org](https://docs.openchain.org/).

This document explains how to run Openchain without using Docker. This process relies on [NuGet](https://www.nuget.org/) to pull the required Openchain packages.

# Prerequisites

Install the [.NET Command Line Interface](https://github.com/dotnet/cli). This is cross-platform and runs on Windows, Linux and OS X.

# Installation

Clone this repository:

``` bash
$ git clone https://github.com/openchain/run.git openchain
```

Restore the dependencies:

``` bash
$ cd openchain
$ dnvm use default
$ dnu restore
```

Run Openchain:

``` bash
$ dnx start
```

# Configuration

## Referencing provider packages

The ``dependencies`` section of the project.json file references the external providers pulled from NuGet:

``` json
"dependencies": {
  "Openchain.Server": "0.5.0-rc1",
  
  "Openchain.Sqlite": "0.5.0-rc1-*",
  "Openchain.Validation.PermissionBased": "0.5.0-rc1-*"
},
```

By defaut, this imports the [Sqlite storage engine](https://www.nuget.org/packages/Openchain.Sqlite) (Openchain.Sqlite) as well as the [permission-based validation engine](https://www.nuget.org/packages/Openchain.Validation.PermissionBased) (Openchain.Validation.PermissionBased). Update this list with the providers you want to use.

Make sure you run ``dnu restore`` again after modifying project.json.

You can then edit the ``Webroot/App_Data/config.json`` file to [reference the providers you want to use](https://docs.openchain.org/en/latest/general/configuration.html).

# Updating the target platform

The ``frameworks`` section of the project.json file lists the available target frameworks:

``` json
"frameworks": {
  "dnxcore50": {},
  "dnx451": {}
}
```

By default .NET Core (cross-platform) and the .NET Framework (Windows only) are both targeted. Some providers run only on a subset of frameworks. In that case, remove the unsupported frameworks from the list.

## License

Copyright 2015 Coinprism, Inc.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
