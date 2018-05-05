---
title: Mediante la creación de reflejo (JDBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7528a85cd8e2eb258a89e6d7971ce0f80fa90258
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-database-mirroring-jdbc"></a>Usar la creación de reflejo de la base de datos (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  La creación de reflejo de la base de datos es un solución de software destinada a aumentar la disponibilidad de la base de datos y la redundancia de los datos. El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ofrece compatibilidad implícita con creación de reflejo de base de datos, por lo que el desarrollador no necesita escribir ningún código ni realizar ninguna otra acción cuando se ha configurado para la base de datos.  
  
 La creación de reflejo, que se implementa en una base de cada base de datos, conserva una copia de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos de producción en un servidor en espera. Este servidor puede ser un servidor en estado de espera activa o semiactiva, dependiendo de la configuración y del estado de la sesión de creación de reflejo de la base de datos. Un servidor en estado de espera activa admite una conmutación por error rápida sin que se produzca una pérdida de las transacciones confirmadas y un servidor en estado de espera semiactiva admite el forzado del servicio (con una posible pérdida de datos).  
  
 La base de datos de producción se llama el *principal* se denomina base de datos y la copia en espera la *reflejado* base de datos. La base de datos principal y la base de datos reflejada deben residir en instancias independientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (instancias de servidor), y deben residir en equipos independientes, si es posible.  
  
 La instancia del servidor de producción, llamado servidor principal, se comunica con la instancia del servidor en espera, llamado servidor reflejado. Los servidores principal y reflejado actúan como asociados en la sesión de creación de reflejo de la base de datos. Si se produce un error en el servidor principal, el servidor reflejado puede convertir su base de datos en la base de datos principal mediante un proceso denominado *conmutación por error*. Por ejemplo, Partner_A y Partner_B son dos servidores asociados, con la base de datos principal inicialmente en Partner_A como servidor principal y la base de datos reflejada en Partner_B como servidor reflejado. Si Partner_A se queda sin conexión, la base de datos de Partner_B puede realizar la conmutación por error para convertirse en la base de datos principal actual. Cuando Partner_A se vuelve a unir a la sesión de creación de reflejo, se convierte en el servidor reflejado y su base de datos pasa a ser la base de datos reflejada.  
  
 En caso de que el servidor Partner_A se dañe de forma irreparable, se puede poner en línea un servidor Partner_C para que actúe como un servidor reflejado para Partner_B, que es ahora el servidor principal. No obstante, en este escenario, la aplicación cliente debe incluir una lógica de programación para asegurarse de que las propiedades de la cadena de conexión se actualizan con los nombres de servidor nuevos usados en la configuración de la creación de reflejo de la base de datos. En caso contrario, es posible que la conexión con los servidores no se realice.  
  
 Las configuraciones alternativas de creación de reflejo de la base de datos proporcionan diferentes niveles de rendimiento y de seguridad de los datos, y admiten varias formas de conmutación por error. Para obtener más información, vea "Información general de Database Mirroring" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="programming-considerations"></a>Consideraciones de programación  
 Cuando el servidor principal genera un error, la aplicación cliente recibe mensajes de error como respuesta a las llamadas a la API que indican que se ha perdido la conexión a la base de datos. En este caso, se pierden todos los cambios sin confirmar introducidos en la base de datos y se revierte la transacción actual. Por lo tanto, la aplicación debe cerrar la conexión (o liberar el objeto de origen de datos) e intentar volver a abrirla. Una vez establecida la conexión, la nueva conexión se redirige de forma transparente a la base de datos reflejada, la cual actúa ahora como el servidor principal sin que el cliente tenga que modificar la cadena de conexión o el objeto de origen de datos.  
  
 Si se ha establecido una conexión al inicio, el servidor principal envía la identidad de su asociado de conmutación por error al cliente que se va a usar al producirse la conmutación por error. Si la aplicación intenta establecer una conexión inicial con un servidor principal que ha generado un error, el cliente no conoce la identidad del asociado de conmutación por error. Para permitir a los clientes la oportunidad de este escenario, la propiedad de cadena de conexión de failoverPartner y, opcionalmente, el [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) del origen de datos (método), permite al cliente especificar la identidad de la conmutación por error socio comercial por sí mismo. La propiedad del cliente se usa solo en este escenario; si el servidor principal está disponible, no se usa.  
  
> [!NOTE]  
>  Si se especifica failoverPartner en la cadena de conexión o con un objeto de origen de datos, la propiedad databaseName también se debe establecer para que no se inicie una excepción. Si failoverPartner y databaseName no se especifican explícitamente, la aplicación no intentará la conmutación por error cuando se produzcan errores en el servidor de base de datos principal. En otras palabras, la redirección transparente solo funciona para las conexiones que especifican explícitamente failoverPartner y databaseName. Para obtener más información acerca de failoverPartner y otras propiedades de cadena de conexión, vea [estableciendo las propiedades de conexión](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Si el servidor asociado de conmutación por error suministrado por el cliente no hace referencia a un servidor que actúa como asociado de conmutación por error para la base de datos especificada, y si el servidor o la base de datos a los que se hace referencia está en una disposición de creación de reflejo de la base de datos, el servidor rechazará la conexión. Aunque la [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase proporciona el [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) método, este método sólo devuelve el nombre del asociado de conmutación por error especificado en la cadena de conexión o el método setFailoverPartner. Para recuperar el nombre del asociado de conmutación por error real que se está usando actualmente, use la siguiente [!INCLUDE[tsql](../../includes/tsql_md.md)] instrucción:  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  Debe cambiar esta instrucción para usar el nombre de la base de datos reflejada.  
  
 Debe tener en cuenta la posibilidad de almacenar en caché la información del asociado para actualizar la cadena de conexión o crear una estrategia de reintento en caso de que el primer intento de conexión no se realice correctamente.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, se realiza un primer intento de conexión con el servidor principal. Si este método genera un error y se devuelve una excepción, se realiza un intento de conexión con el servidor reflejado, que puede haberse convertido en el nuevo servidor principal. Tenga en cuenta el uso de la propiedad failoverPartner en la cadena de conexión.  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Conexión a SQL Server con el controlador JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
