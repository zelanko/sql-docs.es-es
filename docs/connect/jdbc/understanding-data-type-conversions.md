---
title: "Conversiones de tipos de datos de descripción | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b8a4439d9682435baca0867dfc9d8bd96d0fcd7c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-data-type-conversions"></a>Descripción de las conversiones de tipos de datos
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para facilitar la conversión de tipos de datos de lenguaje de programación Java [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona las conversiones de tipo de datos según sea necesario mediante la especificación de JDBC. Para mejorar la flexibilidad, todos los tipos son convertibles de **objeto**, **cadena**, y **byte []** tipos de datos.  
  
## <a name="getter-method-conversions"></a>Conversiones de métodos de captador  
 En función de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos, el gráfico siguiente contiene el mapa de conversión del controlador JDBC para get\<tipo > métodos () de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) (clase) así como las conversiones compatibles para get\< Tipo > métodos de la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clase.  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 Los métodos de captador del controlador JDBC admiten tres categorías de conversiones:  
  
-   **Sin pérdidas (x)**: conversiones para los casos donde el tipo de captador es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a getBigDecimal en una columna decimal del servidor subyacente, no es necesario realizar ninguna conversión.  
  
-   **Convertido (y)**: conversiones de tipos de servidores numéricos a tipos del lenguaje Java que la conversión es normal y sigue las reglas de conversión de lenguaje Java. Para estas conversiones, la precisión siempre se trunca, nunca se redondea, y el desbordamiento se trata como un módulo del tipo de destino, que es más pequeño. Por ejemplo, al llamar a getInt en una subyacente **decimal** columna que contiene "1.9999" devolverá "1", o si subyacente **decimal** valor es "3000000000", a continuación, el **int** valor que se desborda a "-1294967296".  
  
-   **Dependiente de datos (z)**: conversiones de tipos de caracteres subyacentes a tipos numéricos requieren que los tipos de caracteres contengan valores que se pueda convertir a ese tipo. No se realiza ninguna otra conversión. Si el valor es demasiado grande para el tipo de captador, el valor no es válido. Por ejemplo, si se llama a getInt en una columna varchar (50) que contiene "53", el valor se devuelve como un **int**; pero si el valor subyacente es "xyz" o "3000000000", se produce un error.  
  
 Si se llama a getString en un **binario**, **varbinary**, **varbinary (max)**, o **imagen** tipo de datos de columna, el valor se devuelve como un valor de cadena hexadecimal.  
  
## <a name="updater-method-conversions"></a>Conversiones de métodos de actualización  
 Para los tipos de Java pasados a la actualización de datos\<tipo > métodos () de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) (clase), se aplican las conversiones siguientes.  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 Los métodos de actualización del controlador JDBC admiten tres categorías de conversiones:  
  
-   **Sin pérdidas (x)**: conversiones para los casos donde el tipo de actualización es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a updateBigDecimal en una columna decimal del servidor subyacente, no es necesario realizar ninguna conversión.  
  
-   **Convertido (y)**: conversiones de tipos de servidores numéricos a tipos del lenguaje Java que la conversión es normal y sigue las reglas de conversión de lenguaje Java. Para estas conversiones, la precisión siempre se trunca (nunca se redondea) y el desbordamiento se trata como un módulo del tipo de destino (el más pequeño). Por ejemplo, al llamar a updateDecimal en una subyacente **int** columna que contiene "1.9999" devolverá "1", o si subyacente **decimal** valor es "3000000000", a continuación, el **int**valor se desborda a "-1294967296".  
  
-   **Dependiente de datos (z)**: conversiones de tipos de datos de origen subyacentes a tipos de datos de destino requieren que se puedan convertir los valores contenidos en los tipos de destino. No se realiza ninguna otra conversión. Si el valor es demasiado grande para el tipo de captador, el valor no es válido. Por ejemplo, si se llama a updateString en una columna que contiene "53", la actualización se realiza correctamente, pero si el valor String subyacente es "foo" o "3000000000", se genera un error.  
  
 Cuando se llama a updateString en una **binario**, **varbinary**, **varbinary (max)**, o **imagen** tipo de datos de columna, controla el valor de cadena como un valor de cadena hexadecimal.  
  
 Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos de columna **XML**, el valor de datos debe ser válido **XML**. Al llamar a métodos updateBlob, updateBinaryStream o updateBytes, el valor de datos debe ser la representación de cadena hexadecimal de los caracteres XML. Por ejemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.  
  
## <a name="setter-method-conversions"></a>Conversiones del método establecedor  
 Para los tipos de Java pasados al conjunto de datos\<tipo > métodos () de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase y la [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) (clase), se aplican las conversiones siguientes.  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 El servidor intenta realizar las conversiones y devuelve errores si no lo consigue.  
  
 En el caso de los **cadena** tipo de datos, si el valor supera la longitud de **VARCHAR**, que se asigna a **LONGVARCHAR**. De forma similar, **NVARCHAR** se asigna a **LONGNVARCHAR** si el valor supera la longitud admitida de **NVARCHAR**. Lo mismo puede decirse de **byte []**. Valores con más de **VARBINARY** se convierten en **LONGVARBINARY**.  
  
 Los métodos de establecimiento del controlador JDBC admiten dos categorías de conversiones:  
  
-   **Sin pérdidas (x)**: conversiones para los casos numéricos en los que el tipo de establecedor es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a setBigDecimal en un servidor subyacente **decimal** columna, no es necesario realizar ninguna conversión. Numérico a casos de carácter, el Java **numérico** tipo de datos se convierte en una **cadena**. Por ejemplo, al llamar a setDouble con un valor de "53" en una columna varchar (50), produce un valor de carácter "53" en esa columna de destino.  
  
-   **Convertido (y)**: las conversiones de un Java **numérico** tipo a un servidor subyacente **numérico** tipo que sea menor. Esta conversión es normal y sigue [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] convenciones de conversión. Precisión siempre se trunca (nunca se redondea) y el desbordamiento produce un error de conversión no admitida. Por ejemplo, mediante updateDecimal con un valor de "1,9999" en un subyacente entero columna da como resultado un "1" en la columna de destino; pero si se pasa de "3000000000", el controlador produce un error.  
  
-   **Dependiente de datos (z)**: las conversiones de un Java **cadena** tipo subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos depende de las siguientes condiciones: el controlador envía el **cadena** valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] realiza las conversiones si es necesario. Si sendStringParametersAsUnicode se establece en true y subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos **imagen**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no permite la conversión **nvarchar** a **imagen** y genera una excepción SQLServerException. Si sendStringParametersAsUnicode se establece en false y subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos **imagen**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permite la conversión **varchar** a **imagen**y no produce una excepción.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]realiza las conversiones y devuelve errores al controlador JDBC cuando hay problemas.  
  
 Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos de columna **XML**, el valor de datos debe ser válido **XML**. Al llamar a métodos updateBlob, updateBinaryStream o updateBytes, el valor de datos debe ser la representación de cadena hexadecimal de los caracteres XML. Por ejemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.  
  
## <a name="conversions-on-setobject"></a>Conversiones en setObject  
  
> [!NOTE]  
>  Microsoft JDBC Drivers 4.2 (y versiones posteriores) para SQL Server admite JDBC 4.1 y 4.2. Para obtener más detalles sobre 4.1 y 4.2 asignaciones de tipo de datos y las conversiones vea [JDBC 4.1 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md) y [JDBC 4.2 Compliance para el controlador JDBC](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md), además de la información siguiente.  
  
 Para los tipos Java datos que se pasan a la setObject (\<tipo >) métodos de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (clase), se aplican las conversiones siguientes.  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 El método setObject con ningún tipo de destino especificado usará la asignación predeterminada. En el caso de los **cadena** tipo de datos, si el valor supera la longitud de **VARCHAR**, que se asigna a **LONGVARCHAR**. De forma similar, **NVARCHAR** se asigna a **LONGNVARCHAR** si el valor supera la longitud admitida de **NVARCHAR**. Lo mismo puede decirse de **byte []**. Valores con más de **VARBINARY** se convierten en **LONGVARBINARY**.  
  
 Los métodos setObject del controlador JDBC admiten tres categorías de conversiones:  
  
-   **Sin pérdidas (x)**: conversiones para los casos numéricos en los que el tipo de establecedor es igual o menor que el tipo de servidor subyacente. Por ejemplo, al llamar a setBigDecimal en un servidor subyacente **decimal** columna, no es necesario realizar ninguna conversión. Numérico a casos de carácter, el Java **numérico** tipo de datos se convierte en una **cadena**. Por ejemplo, una llamada a setDouble con un valor de "53" en una columna varchar (50) generará un valor de carácter "53" en esa columna de destino.  
  
-   **Convertido (y)**: las conversiones de un Java **numérico** tipo a un servidor subyacente **numérico** tipo que sea menor. Esta conversión es normal y sigue [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] convenciones de conversión. La precisión siempre se trunca, nunca se redondea, y el desbordamiento lanza un error de conversión no admitida. Por ejemplo, mediante updateDecimal con un valor de "1,9999" en un subyacente entero columna da como resultado un "1" en la columna de destino; pero si se pasa de "3000000000", el controlador produce un error.  
  
-   **Dependiente de datos (z)**: las conversiones de un Java **cadena** tipo subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos depende de las siguientes condiciones: el controlador envía el **cadena** valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] realiza las conversiones si es necesario. Si la propiedad de conexión sendStringParametersAsUnicode se establece en true y subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos **imagen**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no permite la conversión **nvarchar** a **imagen** y genera una excepción SQLServerException. Si sendStringParametersAsUnicode se establece en false y subyacente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos **imagen**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permite la conversión **varchar** a **imagen**y no produce una excepción.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]realiza el grueso de las conversiones de establecimiento y devuelve errores al controlador JDBC cuando hay problemas. Las conversiones del lado cliente son la excepción y no se realiza únicamente en el caso de **fecha**, **tiempo**, **timestamp**, **booleano**y ** Cadena** valores.  
  
 Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] es de tipo de datos de columna **XML**, el valor de datos debe ser válido **XML**. Cuando se llama a los métodos setObject(byte[], SQLXML), setObject(inputStream, SQLXML) o setObject(Blob, SQLXML), el valor de los datos debería ser una representación de cadena hexadecimal de los caracteres XML. Por ejemplo:  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 Tenga en cuenta que se necesita una marca de orden de bytes (BOM) si los caracteres XML están en codificaciones de caracteres específicos.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
