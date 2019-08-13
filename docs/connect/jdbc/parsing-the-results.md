---
title: Analizando los resultados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 163055a630f8e37678f99359a244bf211b035e7e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894077"
---
# <a name="parsing-the-results"></a>Análisis de los resultados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En este artículo se describe cómo SQL Server espera que los usuarios procesen por completo los resultados devueltos de cualquier consulta.

## <a name="update-counts-and-result-sets"></a>Recuentos de actualizaciones y conjuntos de resultados

En esta sección se explican los dos resultados más comunes devueltos por SQL Server: recuento de actualizaciones y conjunto de resultados. En general, cualquier consulta que ejecute un usuario hará que se devuelva uno de estos resultados; se espera que los usuarios controlen ambos al procesar los resultados.

El código siguiente es un ejemplo de cómo un usuario puede recorrer en iteración todos los resultados del servidor:
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>Excepciones
Cuando se ejecuta una instrucción que genera un error o un mensaje informativo, SQL Server responderá de manera diferente en función de si puede generar un plan de ejecución. El mensaje de error se puede iniciar inmediatamente después de la ejecución de la instrucción o podría requerir un conjunto de resultados independiente. En el último caso, las aplicaciones deben analizar el conjunto de resultados para recuperar la excepción.

Cuando SQL Server no puede generar un plan de ejecución, la excepción se produce inmediatamente.

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

Cuando SQL Server devuelve un mensaje de error en un conjunto de resultados, el conjunto de resultados debe procesarse para recuperar la excepción.

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

Si la ejecución de la instrucción genera varios conjuntos de resultados, cada conjunto de resultados debe procesarse hasta que se alcance el que tiene la excepción.

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

En el caso de `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`, se produce una excepción inmediatamente `execute()` en `SELECT 1` y no se ejecuta en absoluto.

Si el error de SQL Server tiene una gravedad `0` de `9`a, se considera un mensaje informativo y se devuelve `SQLWarning`como.

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>Vea también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)
