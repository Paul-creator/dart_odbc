# dart_odbc

This is an api library for communicating with the odbc driver from dart
This package is inspired by the original [odbc](https://pub.dev/packages/odbc) (obsolete).

[![style: very good analysis](https://img.shields.io/badge/style-very_good_analysis-B22C89.svg)](https://pub.dev/packages/very_good_analysis)

## Usage

- Instanciate the ODBC class by providing the path to the odbc driver on the host machine

```dart
  final odbc = DartOdbc('/path/to/the/odbc/driver');
```

### Path to ODBC Driver

Path to the ODBC driver can be found in the ODBC driver manager.
In windows this is a `.dll` file that is there in the installation folder of the ODBC driver.
In linux this has an extension of `.so`.
In macos this should have an extension of `.dylib`.

- Connect to the database by providing the DSN (Data Source Name) configured in the ODBC Driver Manager

```dart
  odbc.connect(
    dsn: '<your_dsn>',
    username: 'db_username',
    password: 'db_password',
  );
```

### DSN (Data Source Name)

This is the name you gave when setting up the driver manager.
For more information, visit this page from the [MySQL Documentation](https://dev.mysql.com/doc/connector-odbc/en/connector-odbc-driver-manager.html)

- In case the path privided to the driver is invalid or there is any issue with setting up the environment/connecting to the database, an `Exception` will be thrown when intanciating the ODBC or connecting to the database.
- Execute your queries directly as follows

```dart
  final result = odbc.execute("SELECT 10");
```

- Result will be a `List` of `Map` objects where each Map represents a row. If anything goes wrong an `Exception` will be thrown

### Accessing low level API

- Since this package is at its early stage, most advanced functionalities are not implemented or tested yet. In case you need more functionality, the direct access to the `ODBC` driver can be obtained by importing the `LibODBC` class from `ffi/libodbc.dart`.

- For more information on the `ODBC` api go to [Microsoft ODBC Documentation](https://learn.microsoft.com/en-us/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-ver16)

TODO:

- [X] Implement query sanitization
- [X] Do more testing on different databases
  - [X] MS SQL Server
  - [X] Oracle server
- [ ] Improve documentation
