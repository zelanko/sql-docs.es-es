---
title: Ejemplo de origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 166cc1aa7764a310d7cc6741afcd3e4dce3f2f62
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787068"
---
# <a name="data-source-sample"></a>Ejemplo de origen de datos

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo conectar con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un objeto de origen de datos. Además, se muestra cómo recuperar datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un procedimiento almacenado.

El archivo de código para este ejemplo se llama ConnectDataSource.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código establece varias propiedades de conexión con métodos establecedores del objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) y, después, llama al método [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) del objeto SQLServerDataSource para devolver un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).

Después, el código muestra usa el método [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) del objeto SQLServerConnection para crear un objeto [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) y, luego, se llama al método [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) para ejecutar el procedimiento almacenado.

Finalmente, el ejemplo usa el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) devuelto por el método executeQuery para procesar una iteración mediante los resultados devueltos por el procedimiento almacenado.

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(Integer.parseInt("<port>"));
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>Ver también

[Conexión y recuperación de datos](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
