---
title: Contenedores e Interfaces | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cee557293ccc5949977f0d3a9225ba0ea3d018d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="wrappers-and-interfaces"></a>Contenedores e interfaces
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite interfaces que permiten crear un proxy de una clase y contenedores que permiten tener acceso a las extensiones para la API de JDBC que son específicas de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] a través de una interfaz de proxy.  
  
## <a name="wrappers"></a>Controladores  
 El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] es compatible con la interfaz java.sql.Wrapper. Esta interfaz proporciona un mecanismo para las extensiones de acceso a la API de JDBC que son específicos de la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] a través de una interfaz de proxy.  
  
 La interfaz java.sql.Wrapper define dos métodos: **isWrapperFor** y **unwrap**. El **isWrapperFor** método comprueba si el objeto de entrada especificado implementa esta interfaz. El **unwrap** método devuelve un objeto que implementa esta interfaz para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos específicos.  
  
 **isWrapperFor** y **unwrap** métodos se exponen como sigue:  
  
-   [Método isWrapperFor &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [Método Unwrap &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [Método isWrapperFor &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [Método Unwrap &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [Método isWrapperFor &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [Método Unwrap &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [Método isWrapperFor &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [Método Unwrap &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [Método isWrapperFor &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [Método Unwrap &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [Método isWrapperFor &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [Método Unwrap &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>Interfaces  
 A partir de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] controlador JDBC 3.0, interfaces están disponibles para un servidor de aplicaciones tener acceso a un método específico del controlador de la clase asociada. El servidor de aplicaciones puede incluir la clase mediante la creación de un proxy, exponer el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-funcionalidad específica de una interfaz. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite interfaces que tienen la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] determinados métodos y constantes para un servidor de aplicaciones pueda crear un proxy de la clase.  
  
 Las interfaces se derivan de interfaces de Java para que pueda usar el mismo objeto una vez se haya desencapsulado para tener acceso a funcionalidad específica del controlador o genérico estándar [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] funcionalidad.  
  
 Se agregaron las siguientes interfaces:  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Description  
 Este ejemplo muestra cómo obtener acceso a un [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-función específica de un objeto de origen de datos. Esta clase de origen de datos que se ajustaron mediante un servidor de aplicaciones. Para obtener acceso a la función específica del controlador JDBC o constante, puede desencapsular el origen de datos a una interfaz ISQLServerDataSource y utilizar las funciones declaradas en esta interfaz.  
  
### <a name="code"></a>código  
  
```  
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
  
## <a name="see-also"></a>Vea también  
 [Describir los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
