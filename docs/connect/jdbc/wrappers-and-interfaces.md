---
title: Contenedores e Interfaces | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad3412a5d296a7d243d6b73b6275c613da5c962b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783944"
---
# <a name="wrappers-and-interfaces"></a>Contenedores e interfaces

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite interfaces que permiten crear un proxy de una clase y contenedores que permiten acceder a extensiones para la API de JDBC que son específicas de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] mediante una interfaz de proxy.

## <a name="wrappers"></a>Controladores

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite la interfaz java.sql.Wrapper. Esta interfaz proporciona un mecanismo para acceder a extensiones para la API de JDBC que son específicas de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] mediante una interfaz de proxy.

La interfaz java.sql.Wrapper define dos métodos: **isWrapperFor** y **unwrap**. El método **isWrapperFor** comprueba si el objeto de entrada especificado implementa esta interfaz. El método **unwrap** devuelve un objeto que implementa esta interfaz para permitir el acceso a los métodos específicos de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

**isWrapperFor** y **unwrap** métodos se exponen como sigue:

- [Método isWrapperFor &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [Método unwrap &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [Método isWrapperFor &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [Método unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [Método Unwrap &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [Método isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [Método unwrap &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [Método isWrapperFor &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [Método Unwrap &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [Método isWrapperFor &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [Método Unwrap &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>Interfaces

A partir de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0, las interfaces están disponibles para que un servidor de aplicaciones acceda a un método específico del controlador desde la clase asociada. El servidor de aplicaciones puede incluir la clase si crea un proxy, de forma que se exponga la funcionalidad específica de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] desde una interfaz. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite interfaces que tienen los métodos y constantes propios de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], de forma que un servidor de aplicaciones pueda crear un proxy de la clase.

Las interfaces se derivan de interfaces de Java estándar, por lo que se puede usar el mismo objeto una vez que se haya desencapsulado para acceder a funcionalidad específica del controlador o a funcionalidad genérica de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].

Se agregaron las siguientes interfaces:

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>Ejemplo

### <a name="description"></a>Descripción

En este ejemplo se muestra cómo acceder a una función específica de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] desde un objeto DataSource. Es posible que un servidor de aplicaciones haya encapsulado esta clase DataSource. Para acceder a la función o constante específica del controlador JDBC, puede desencapsular el origen de datos en una interfaz ISQLServerDataSource y usar las funciones que se declaran en esta interfaz.

### <a name="code"></a>código

```java
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  

public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  

   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  

         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  

      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```

## <a name="see-also"></a>Ver también

[Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
