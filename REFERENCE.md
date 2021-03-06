# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

* [`influxdb`](#influxdb): Main class that ties the module together
* [`influxdb::config`](#influxdbconfig): Manages the configuration of InfluxDB
* [`influxdb::install`](#influxdbinstall): Manages the installation of InfluxDB
* [`influxdb::service`](#influxdbservice): Manages the service of InfluxDB

**Defined types**

* [`influxdb::database`](#influxdbdatabase): Manages a database within InfluxDB
* [`influxdb::user`](#influxdbuser): Manages a user within InfluxDB

**Resource types**

* [`influxdb_auth`](#influxdb_auth): Setup http_auth in InfluxDB.
* [`influxdb_database`](#influxdb_database): Create or update a database in InfluxDB.
* [`influxdb_user`](#influxdb_user): Create or update a user in InfluxDB.

## Classes

### influxdb

Manages InfluxDB

#### Examples

##### 

```puppet
class { '::influxdb':
  admin_username => $admin_username,
  admin_password => $admin_password,
}

class { '::influxdb':
  admin_username => $admin_username,
  admin_password => $admin_password,
  configuration  => {
    'data'  => {
      'dir'                     => '/mnt/influxdb/data',
      'wal-dir'                 => '/mnt/influxdb/wal',
      'max-series-per-database' => 0,
      'max-values-per-tag'      => 0,
    }
  }
}
```

#### Parameters

The following parameters are available in the `influxdb` class.

##### `ensure`

Data type: `Enum['present','absent']`

- Whether to create or destroy this resource

Default value: 'present'

##### `ensure_package`

Data type: `Variant[String,Undef]`

- Overwrite $ensure for the package only. Used if package needs to be anything but 'present' or 'absent'

Default value: `undef`

##### `admin_password`

Data type: `String`

- The password used for the main admin account

##### `admin_username`

Data type: `String`

- The username used for the main admin account

##### `configuration`

Data type: `Hash`

- The configuration to use. Default values will be provided for everything not written

Default value: {}

##### `api_port`

Data type: `Integer`

- The port which to connect to InfluxDB

Default value: 8086

##### `config_path`

Data type: `String`

- The path to the main configuration file

Default value: '/etc/influxdb/influxdb.conf'

##### `group`

Data type: `String`

- The group used for permission on for everything

Default value: 'influxdb'

##### `owner`

Data type: `String`

- The owner used for permission on for everything

Default value: 'influxdb'

### influxdb::config

Manages the configuration of InfluxDB

#### Examples

##### 

```puppet
Use main class
```

### influxdb::install

Manages the installation of InfluxDB

#### Examples

##### 

```puppet
Use main class
```

### influxdb::service

Manages the service of InfluxDB

#### Examples

##### 

```puppet
Use main class
```

## Defined types

### influxdb::database

Creates or destroys a database within InfluxDB

#### Examples

##### 

```puppet
influxdb::database { 'my_database_name': }
```

#### Parameters

The following parameters are available in the `influxdb::database` defined type.

##### `ensure`

Data type: `Enum['present','absent']`

- Create or destroy database

Default value: 'present'

##### `name`

- (namevar) The name of the database

##### `admin_password`

Data type: `String`



Default value: $influxdb::admin_password

##### `admin_username`

Data type: `String`



Default value: $influxdb::admin_username

### influxdb::user

Create, destroy or update a user within InfluxDB

#### Examples

##### 

```puppet
influxdb::user { 'read_only_user':
  password  => 'mySuperSecretPassWORD',
  privilege => 'READ',
  database  => 'my_database',
}

influxdb::user { 'admin2':
  password => 'Admin?Need?Better&Password',
  is_admin => true,
}
```

#### Parameters

The following parameters are available in the `influxdb::user` defined type.

##### `privilege`

Data type: `Variant[Enum['READ', 'WRITE', 'ALL'],Undef]`

- What privileges to give the user

Default value: `undef`

##### `is_admin`

Data type: `Boolean`

- Whether the user should be created as an admin or not

Default value: `false`

##### `ensure`

Data type: `Enum['present','absent']`

- Create or destroy user

Default value: 'present'

##### `database`

Data type: `Variant[String,Undef]`

- What database the user should have $privileges too (only for non-admins)

Default value: `undef`

##### `password`

Data type: `Variant[String,Undef]`

- The plain-text password to give the user

Default value: `undef`

##### `name`

- (namevar) The username of the user

##### `admin_password`

Data type: `String`



Default value: $influxdb::admin_password

##### `admin_username`

Data type: `String`



Default value: $influxdb::admin_username

## Resource types

### influxdb_auth

Setup http_auth in InfluxDB.

#### Properties

The following properties are available in the `influxdb_auth` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `influxdb_auth` type.

##### `name`

namevar

A unique name for the resource

##### `admin_username`

Admin username to manage the resource with

##### `admin_password`

Admin password to manage the resource with

##### `config_path`

Path to the main config file

### influxdb_database

Create or update a database in InfluxDB.

#### Properties

The following properties are available in the `influxdb_database` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `influxdb_database` type.

##### `name`

namevar

A unique name for the resource

##### `admin_username`

Admin username to manage the resource with

##### `admin_password`

Admin password to manage the resource with

##### `database`

The database to create

### influxdb_user

Create or update a user in InfluxDB.

#### Properties

The following properties are available in the `influxdb_user` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `privilege`

Which privilege to use

#### Parameters

The following parameters are available in the `influxdb_user` type.

##### `name`

namevar

A unique name for the resource

##### `admin_username`

Admin username to manage the resource with

##### `admin_password`

Admin password to manage the resource with

##### `username`

The user to create

##### `password`

Password for the user to create

##### `is_admin`

Whether to user is a admin or normal user

##### `database`

Which database to grant access to

