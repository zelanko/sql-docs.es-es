---
title: Descripción de las conversiones de tipos de datos
description: Obtenga información sobre cómo el controlador JDBC para SQL Server controla las conversiones de tipos de datos entre los tipos de datos de JDBC y de base de datos.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 266db3efac0fb737ccb36900ef3b27f24c8c8888
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081684"
---
# <a name="understanding-data-type-conversions"></a>Descripción de las conversiones de tipos de datos

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para facilitar la conversión de tipos de datos del lenguaje de programación Java a tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona las conversiones de tipos de datos que necesita la especificación JDBC. Para mejorar la flexibilidad, todos los tipos son convertibles entre los tipos de datos **Object**, **String** y **byte[]**.

## <a name="getter-method-conversions"></a>Conversiones del método Getter

Según los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el siguiente gráfico contiene el mapa de conversión del controlador JDBC para los métodos get\<Type>() de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), así como las conversiones admitidas para los métodos get\<Type> de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md).

![Matriz de conversión de tipos de JDBC a SQL Server](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")

Los métodos de captador del controlador JDBC admiten tres categorías de conversiones:

- **Sin pérdidas (x)**: conversiones para los casos en los que el tipo de captador es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a getBigDecimal en una columna decimal del servidor subyacente, no es necesario realizar ninguna conversión.

- **Convertido (y)**: conversiones desde tipos de servidores numéricos a tipos del lenguaje Java en las que la conversión es normal y sigue las reglas de conversión del lenguaje Java. Para estas conversiones, la precisión siempre se trunca, nunca se redondea, y el desbordamiento se trata como un módulo del tipo de destino, que es más pequeño. Por ejemplo, al llamar a getInt en una columna **decimal** subyacente que contiene "1,9999", por ejemplo, se devolverá "1" o si el valor **decimal** subyacente es "3000000000", el valor **int** se desborda a "-1294967296".

- **Dependiente de datos (z)**: las conversiones de tipos de caracteres subyacentes a tipos numéricos requieren que los tipos de caracteres contengan valores que se puedan convertir a ese tipo. No se realiza ninguna otra conversión. Si el valor es demasiado grande para el tipo de captador, el valor no es válido. Por ejemplo, si se llama a getInt en una columna varchar(50) que contiene "53", el valor se devuelve como **int**, pero si el valor subyacente es "xyz" o "3000000000", se produce un error.

Si se llama a getString en un tipo de datos de la columna **binary**, **varbinary**, **varbinary(max)** o **image**, el valor se devuelve como valor de cadena hexadecimal.

## <a name="updater-method-conversions"></a>Conversiones del método Updater

Para los datos de tipo Java pasados a los métodos update\<Type>() de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md), se aplican las conversiones siguientes.

![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")

Los métodos de actualización del controlador JDBC admiten tres categorías de conversiones:

- **Sin pérdidas (x)**: conversiones para los casos en los que el tipo de actualizador es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a updateBigDecimal en una columna decimal del servidor subyacente, no es necesario realizar ninguna conversión.

- **Convertido (y)**: conversiones desde tipos de servidores numéricos a tipos del lenguaje Java en las que la conversión es normal y sigue las reglas de conversión del lenguaje Java. Para estas conversiones, la precisión siempre se trunca (nunca se redondea) y el desbordamiento se trata como un módulo del tipo de destino (el más pequeño). Por ejemplo, al llamar a updateDecimal en una columna **int** subyacente que contiene "1,9999", por ejemplo, se devolverá "1" o si el valor **decimal** subyacente es "3000000000", el valor **int** se desborda a "-1294967296".

- **Dependiente de datos (z)**: las conversiones de tipos de datos de origen subyacentes a tipos de datos de destino requieren que los valores contenidos se puedan convertir a los tipos de destino. No se realiza ninguna otra conversión. Si el valor es demasiado grande para el tipo de captador, el valor no es válido. Por ejemplo, si se llama a updateString en una columna que contiene "53", la actualización se realiza correctamente, pero si el valor String subyacente es "foo" o "3000000000", se genera un error.

Al llamarse a updateString en un tipo de datos de la columna **binary**, **varbinary**, **varbinary(max)** o **image**, controla el valor String como valor de cadena hexadecimal.

Cuando el tipo de datos de columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es **XML**, el valor de los datos debe ser un tipo **XML** válido. Cuando se llama a los métodos updateBytes, updateBinaryStream o updateBlob, el valor de los datos debe ser la representación de la cadena hexadecimal de los caracteres XML. Por ejemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.

## <a name="setter-method-conversions"></a>Conversiones del método Setter

Para los datos de tipo Java pasados a los métodos set\<Type>() de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y de la clase [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), se aplican las siguientes conversiones.

![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")

El servidor intenta realizar las conversiones y devuelve errores si no lo consigue.

En el caso del tipo de datos **String**, si el valor supera la longitud de**VARCHAR**, se asigna a **LONGVARCHAR**. Del mismo modo, **NVARCHAR** se asigna a **LONGNVARCHAR** si el valor supera la longitud admitida de **NVARCHAR**. Lo mismo sucede para **byte[]**. Los valores mayores que **VARBINARY** pasan a ser **LONGVARBINARY**.

Los métodos de establecimiento del controlador JDBC admiten dos categorías de conversiones:

- **Sin pérdidas (x)**: conversiones para los casos numéricos en los que el tipo de establecedor es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a setBigDecimal en una columna **decimal** del servidor subyacente, no es necesario realizar ninguna conversión. En los casos de conversión de tipo numérico a carácter, el tipo de datos **numérico** de Java se convierte en **String**. Por ejemplo, si se llama a setDouble con el valor "53" en una columna varchar(50), se producirá un valor de carácter "53" en esa columna de destino.

- **Convertido (y)** : Conversiones de un tipo **numeric** de Java a un tipo **numeric** del servidor subyacente que es menor. Esta conversión es normal y sigue las convenciones de conversión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisión siempre se trunca, nunca se redondea, y el desbordamiento lanza un error de conversión no admitida. Por ejemplo, si se usa updateDecimal con un valor de "1,9999" en una columna subyacente de enteros, el resultado es "1" en la columna destino; pero si se pasa "3000000000", el controlador lanzará un error.

- **Dependiente de datos (z)** : Las conversiones de un tipo **String** de Java a un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente depende de las condiciones siguientes: El controlador envía el valor **String** a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza las conversiones si es necesario. Si la propiedad de conexión sendStringParametersAsUnicode se establece en true y el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente es **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la conversión de **nvarchar** en **image** y genera una SQLServerException. Si sendStringParametersAsUnicode se establece en false y el tipo de datos subyacente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite la conversión de **varchar** en **image** y no genera ninguna excepción.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza las conversiones y devuelve los errores a JDBC Driver cuando hay problemas.

Cuando el tipo de datos de columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es **XML**, el valor de los datos debe ser un tipo **XML** válido. Cuando se llama a los métodos updateBytes, updateBinaryStream o updateBlob, el valor de los datos debe ser la representación de la cadena hexadecimal de los caracteres XML. Por ejemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.

## <a name="conversions-on-setobject"></a>Conversiones en setObject

> [!NOTE]  
> Microsoft JDBC Driver 4.2 (y versiones posteriores) para SQL Server admite JDBC 4.1 y 4.2. Para obtener más información sobre las conversiones y asignaciones de tipos de datos 4.1 y 4.2, consulte [Cumplimiento de JDBC 4.1 con el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [Cumplimiento de JDBC 4.2 con el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), además de la información que se muestra a continuación.

Para los datos de tipo Java pasados a los métodos setObject(\<Type>) de la clase [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), se aplican las conversiones siguientes.

![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")

El método setObject sin un tipo de destino especificado usará la asignación predeterminada. En el caso del tipo de datos **String**, si el valor supera la longitud de**VARCHAR**, se asigna a **LONGVARCHAR**. Del mismo modo, **NVARCHAR** se asigna a **LONGNVARCHAR** si el valor supera la longitud admitida de **NVARCHAR**. Lo mismo sucede para **byte[]**. Los valores mayores que **VARBINARY** pasan a ser **LONGVARBINARY**.

Los métodos setObject del controlador JDBC admiten tres categorías de conversiones:

- **Sin pérdidas (x)**: conversiones para los casos numéricos en los que el tipo de establecedor es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a setBigDecimal en una columna **decimal** del servidor subyacente, no es necesario realizar ninguna conversión. En los casos de conversión de tipo numérico a carácter, el tipo de datos **numérico** de Java se convierte en **String**. Por ejemplo, si se llama a setDouble con el valor "53" en una columna varchar(50), se producirá un valor de carácter "53" en esa columna de destino.

- **Convertido (y)** : Conversiones de un tipo **numeric** de Java a un tipo **numeric** del servidor subyacente que es menor. Esta conversión es normal y sigue las convenciones de conversión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La precisión siempre se trunca, nunca se redondea, y el desbordamiento lanza un error de conversión no admitida. Por ejemplo, si se usa updateDecimal con un valor de "1,9999" en una columna subyacente de enteros, el resultado es "1" en la columna destino; pero si se pasa "3000000000", el controlador lanzará un error.

- **Dependiente de datos (z)** : Las conversiones de un tipo **String** de Java a un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente depende de las condiciones siguientes: El controlador envía el valor **String** a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza las conversiones si es necesario. Si la propiedad de conexión sendStringParametersAsUnicode se configura en true y el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente es **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la conversión de **nvarchar** en **image** y genera una SQLServerException. Si sendStringParametersAsUnicode se establece en false y el tipo de datos subyacente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es **image**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite la conversión de **varchar** en **image** y no genera ninguna excepción.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza el grueso de las conversiones de establecimiento y devuelve errores a JDBC Driver cuando encuentra problemas. Las conversiones del lado cliente son la excepción y solamente se realizan en el caso de los valores **date**, **time**, **timestamp**, **Boolean** y **String**.

Cuando el tipo de datos de columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es **XML**, el valor de los datos debe ser un tipo **XML** válido. Cuando se llama a los métodos setObject(byte[], SQLXML), setObject(inputStream, SQLXML) o setObject(Blob, SQLXML), el valor de los datos debería ser una representación de cadena hexadecimal de los caracteres XML. Por ejemplo:

```xml
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E
```

Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.

## <a name="see-also"></a>Consulte también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
