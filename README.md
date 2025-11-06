## Startup:

#### Configuration:

In ConfigClass change username and password to your ones:
```java
public class ConfigClass {
    private static Connection connection;
    private Statement statement;

    private static String driver = "com.mysql.cj.jdbc.Driver";
    private static String username = "root";
    private static String password = "root";
    private static String url = "jdbc:mysql://localhost:3306/testdb";
    public ConfigClass() throws ClassNotFoundException, SQLException {
        Class.forName(driver);
        connection = DriverManager.getConnection(url, username, password);
        statement = connection.createStatement();
    }

    public static Connection getConnection() {
        return connection;
    }

    public void closeConnection() throws SQLException {
        connection.close();
    }
}
```

---
### If you want to change DB to Postgres

In pom.xml replace this:
```xml
    <dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.0.33</version>
</dependency>
```

with this:
```xml
    <dependency>
    <groupId>org.postgresql</groupId>
      <artifactId>postgresql</artifactId>
      <version>42.7.8</version>
    </dependency>
```
---

#### DB initialization:

##### For MySQL:

> [!note]
> Execute it through CMD, not PowerShell

```bash
mysql -u <your_user_name> -p < <path_to_file_on_your_pc>/initDB.sql
mysql -u <your_user_name> -p < <path_to_file_on_your_pc>/populateDB.sql
```

How the command looks on my pc (i'm in the project's directory):
```bash
mysql -u root -p < src/main/resources/initDB.sql
mysql -u root -p < src/main/resources/populateDB.sql
```

##### For Postgres:

```bash
psql -U <your_user_name> -f <path_to_file_on_your_pc>/initDBForPostgres.sql
```

How the command looks on my pc (i'm in the project's directory):
```bash
psql -U postgres -f src/main/resources/initDBForPostgres.sql
```

---

