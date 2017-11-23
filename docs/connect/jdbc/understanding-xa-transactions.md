---
title: "Descripción de las transacciones XA | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: "80"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6599312aa6c25275e6b7a642c6764591d1bf4cba
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-xa-transactions"></a>Descripción de las transacciones XA
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona compatibilidad para Java Platform, Enterprise Edition/JDBC 2.0 de transacciones distribuidas opcionales. Las conexiones JDBC obtenidas de la [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) clase puede participar en entornos como Java Platform, servidores de aplicaciones de Enterprise Edition (Java EE) de procesamiento de transacciones distribuidas estándar.  
  
> [!WARNING]  
>  Microsoft JDBC Driver 4.2 (y versiones posterior) para SQL incluye nuevas opciones de tiempo de espera para la característica de reversión automática existente de transacciones no preparadas. Vea [configuración de tiempo de espera del servidor para la reversión automática de transacciones no preparadas](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) más adelante en este tema para obtener más detalles.  
  
## <a name="remarks"></a>Comentarios  
 Las clases para la implementación de las transacciones distribuidas son las siguientes:  
  
|Clase|Implementaciones|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|La fábrica de clases para conexiones distribuidas.|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|El adaptador de recursos para el administrador de transacciones.|  
  
> [!NOTE]  
>  Las conexiones de transacciones distribuidas XA se establecen de forma predeterminada en el nivel de aislamiento Read Committed.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>Instrucciones y limitaciones cuando se usan transacciones XA  
 Las siguientes instrucciones adicionales se aplican a las transacciones fuertemente acopladas:  
  
-   Cuando utiliza transacciones XA junto con MS DTC, puede observar que la versión actual de Microsoft DTC (Coordinador de transacciones distribuidas) no admite el comportamiento de bifurcación XA estrechamente acoplado. Por ejemplo, MS DTC tiene una asignación unívoca entre un identificador de rama de transacción XA (XID) y un identificador de transacción de MS DTC, y el trabajo que realizan las bifurcaciones XA débilmente acopladas se aísla entre estas.  
  
     La revisión que se proporciona en [MSDTC and Tightly Coupled Transactions](http://support.microsoft.com/kb/938653) habilita la compatibilidad con bifurcaciones XA estrechamente acopladas que varias bifurcaciones XA con el mismo identificador (GTRID) de transacción global se asignan a un único identificador de transacción de MS DTC. Esta compatibilidad habilita varias bifurcaciones XA fuertemente acopladas comprobar los cambios de los demás en el Administrador de recursos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   A [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) marca permite que las aplicaciones usen transacciones XA estrechamente acopladas, que tienen diferentes rama de transacción XA identificadores (BQUAL), pero la misma transacción global (GTRID) de identificador e identificador de formato (FormatID). Para usar esta característica, debe establecer el [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) en el parámetro flags del método XAResource.start:  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>Instrucciones de configuración  
 Los siguientes pasos son necesarios si desea usar los orígenes de datos XA junto con Microsoft DTC (Coordinador de transacciones distribuidas) para administrar las transacciones distribuidas.  
  
> [!NOTE]  
>  Los componentes de transacciones distribuidas de JDBC están incluidos en el directorio xa de la instalación del controlador JDBC. Estos componentes incluyen los archivos xa_install.sql y sqljdbc_xa.dll.  
  
### <a name="running-the-ms-dtc-service"></a>Ejecutar el servicio MS DTC  
 El servicio MS DTC debe marcarse **automática** en el Administrador de servicios para asegurarse de que se esté ejecutando cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se ha iniciado el servicio. Para habilitar Microsoft DTC (Coordinador de transacciones distribuidas) para las transacciones XA, debe seguir estos pasos:  
  
 En Windows Vista y versiones posteriores:  
  
1.  Haga clic en el **iniciar** , escriba **dcomcnfg** en el inicio **búsqueda** cuadro y, a continuación, presione ENTRAR para abrir **servicios de componentes**. También puede escribir %windir%\system32\comexp.msc en el **Iniciarbúsqueda** cuadro para abrir **servicios de componentes**.  
  
2.  Expanda Servicios de componentes, Equipos, Mi PC y Microsoft DTC (Coordinador de transacciones distribuidas).  
  
3.  Haga clic en **DTC Local** y, a continuación, seleccione **propiedades**.  
  
4.  Haga clic en el **seguridad** pestaña en el **propiedades de DTC Local** cuadro de diálogo.  
  
5.  Seleccione el **Habilitar transacciones XA** casilla de verificación y, a continuación, haga clic en **Aceptar**. De este modo, se reinicia el servicio MS DTC.  
  
6.  Haga clic en **Aceptar** otra vez para cerrar el **propiedades** cuadro de diálogo y, a continuación, cierre **servicios de componentes**.  
  
7.  Detenga y reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para asegurarse de que se sincroniza con los cambios de MS DTC.  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>Configurar los componentes de transacciones distribuidas de JDBC  
 Puede configurar los componentes de transacciones distribuidas del controlador JDBC mediante estos pasos:  
  
1.  Copie el nuevo archivo sqljdbc_xa.dll desde el directorio de instalación del controlador JDBC al directorio Binn de cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] equipo que vaya a participar en transacciones distribuidas.  
  
    > [!NOTE]  
    >  Si usa transacciones XA con 32 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], utilice el archivo sqljdbc_xa.dll de la x86 carpeta, incluso si la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está instalado en un x64 procesador. Si usa transacciones XA con 64 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en la x64 procesador, utilice el archivo sqljdbc_xa.dll de la x64 carpeta.  
  
2.  Ejecute el script de base de datos xa_install.sql en cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia que vaya a participar en transacciones distribuidas. Este script instala los procedimientos almacenados extendidos que son llamados por sqljdbc_xa.dll. Estos procedimientos almacenados extendidos implementan la transacción distribuida y la compatibilidad con XA el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Debe ejecutar esta secuencia de comandos como administrador de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia.  
  
3.  Para conceder permisos a un usuario concreto de modo que pueda participar en las transacciones distribuidas con el controlador JDBC, agregue el usuario al rol SqlJDBCXAUser.  
  
 Puede configurar solo una versión del ensamblado sqljdbc_xa.dll en cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia a la vez. Las aplicaciones pueden necesitar usar diferentes versiones del controlador JDBC para conectar con la misma [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia mediante la conexión XA. En ese caso, sqljdbc_xa.dll, que se incluye con el controlador JDBC más reciente, debe instalarse en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia.  
  
 Hay tres maneras de comprobar la versión de sqljdbc_xa.dll está actualmente instalada en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia:  
  
1.  Abra el directorio de registro del [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] equipo que vaya a participar en transacciones distribuidas. Seleccione y abra la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] archivo "ERRORLOG". Busque la frase "Using 'SQLJDBC_XA.dll' version ..." en el archivo "ERRORLOG".  
  
2.  Abra el directorio Binn de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] equipo que vaya a participar en transacciones distribuidas. Seleccione el ensamblado sqljdbc_xa.dll.  
  
    -   En Windows Vista o versiones posteriores, haga clic con el botón secundario en sqljdbc_xa.dll y, a continuación, seleccione Propiedades. A continuación, haga clic en el **detalles** ficha. El **versión del archivo** campo muestra la versión de sqljdbc_xa.dll está actualmente instalada en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instancia.  
  
3.  Configure la funcionalidad de registro tal como se muestra en el ejemplo de código de la sección siguiente. Busque la frase "Server XA DLL version:..." en el archivo de registro de resultados.  
  
###  <a name="BKMK_ServerSide"></a>Configuración de tiempo de espera del servidor para la reversión automática de transacciones no preparadas  
  
> [!WARNING]  
>  Esta opción de servidor es nueva con Microsoft JDBC Driver 4.2 (y versiones posteriores) para SQL Server. Para obtener el comportamiento actualizado, asegúrese de que se actualiza sqljdbc_xa.dll en el servidor. Para obtener más información acerca de cómo establecer los tiempos de espera del lado de cliente, consulte [XAResource.settransactiontimeout ()](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html).  
  
 Hay dos configuraciones de registro (valores DWORD) para controlar el comportamiento de tiempo de espera de las transacciones distribuidas:  
  
-   **XADefaultTimeout** (en segundos): el valor de tiempo de espera predeterminado que se utilizará cuando el usuario no especifica ningún tiempo de espera. El valor predeterminado es 0.  
  
-   **XAMaxTimeout** (en segundos): el valor máximo de tiempo de espera que un usuario puede establecer. El valor predeterminado es 0.  
  
 Estos valores son específicos de la instancia de SQL Server y se deben crear en la siguiente clave del registro:  
  
 HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\MSSQL\<**versión**>.\< *instance_name*> \XATimeout  
  
> [!NOTE]  
>  Para 32 bits SQL Server en equipos de 64 bits, se debe crear la configuración del registro en la siguiente clave: HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL\<versión >. < nombre_instancia > \ XATimeout  
  
 Cuando se inicia, se establece un valor de tiempo de espera para cada transacción y el servidor SQL revierte la transacción si expira el tiempo de espera. El tiempo de espera se determina en función de esta configuración del registro y de lo que el usuario haya especificado a través de XAResource.setTransactionTimeout(). A continuación se muestran algunos ejemplos de cómo se interpretan estos valores de tiempo de espera:  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 0  
  
     Significa que no se usará ningún tiempo de espera predeterminado y tampoco se exigirá que los clientes establezcan un tiempo de espera máximo. En este caso, las transacciones tendrán un tiempo de espera solo si el cliente establece un tiempo de espera mediante XAResource.setTransactionTimeout.  
  
-   XADefaultTimeout = 60, XAMaxTimeout = 0  
  
     Significa que todas las transacciones tendrán un tiempo de espera de 60 segundos si el cliente no especifica ningún tiempo de espera. Si el cliente especifica un tiempo de espera, entonces se usará ese valor de tiempo de espera. No se exige ningún valor máximo para el tiempo de espera.  
  
-   XADefaultTimeout = 30, XAMaxTimeout = 60  
  
     Significa que todas las transacciones tendrán un tiempo de espera de 30 segundos si el cliente no especifica ningún tiempo de espera. Si el cliente especifica algún tiempo de espera, entonces se usará el tiempo de espera del cliente siempre y cuando sea inferior a 60 segundos (el valor máximo).  
  
-   XADefaultTimeout = 0, XAMaxTimeout = 30  
  
     Significa que todas las transacciones tendrán un tiempo de espera de 30 segundos (el valor máximo) si el cliente no especifica ningún tiempo de espera. Si el cliente especifica algún tiempo de espera, entonces se usará el tiempo de espera del cliente siempre y cuando sea inferior a 30 segundos (el valor máximo).  
  
### <a name="upgrading-sqljdbcxadll"></a>Actualización de sqljdbc_xa.dll  
 Al instalar una nueva versión del controlador JDBC, también debe usar sqljdbc_xa.dll de la nueva versión para actualizar sqljdbc_xa.dll en el servidor.  
  
> [!IMPORTANT]  
>  Debe actualizar sqljdbc_xa.dll durante un intervalo de mantenimiento o cuando no haya transacciones MS DTC en curso.  
  
1.  Descargue sqljdbc_xa.dll con el [!INCLUDE[tsql](../../includes/tsql_md.md)] comando **DBCC sqljdbc_xa (FREE)**.  
  
2.  Copie el nuevo archivo sqljdbc_xa.dll desde el directorio de instalación del controlador JDBC al directorio Binn de cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] equipo que vaya a participar en transacciones distribuidas.  
  
     La nueva DLL se cargará cuando se llame a un procedimiento extendido en sqljdbc_xa.dll. No es necesario reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para cargar las definiciones nuevas.  
  
### <a name="configuring-the-user-defined-roles"></a>Configurar los roles definidos por el usuario  
 Para conceder permisos a un usuario concreto de modo que pueda participar en las transacciones distribuidas con el controlador JDBC, agregue el usuario al rol SqlJDBCXAUser. Por ejemplo, use la siguiente [!INCLUDE[tsql](../../includes/tsql_md.md)] código para agregar un usuario denominado 'shelby' (usuario de inicio de sesión estándar de SQL denominado 'shelby') al rol SqlJDBCXAUser:  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 Los roles definidos por el usuario de SQL se definen para cada base de datos. Para crear su propio rol por motivos de seguridad, debe definir el rol en cada base de datos y agregar los usuarios para cada base de datos. El rol SqlJDBCXAUser se define estrictamente en la base de datos maestra porque se utiliza para conceder acceso a los procedimientos almacenados extendidos del controlador JDBC de SQL que se encuentran en la base de datos maestra. En primer lugar, debe conceder acceso a cada usuario a la base de datos maestra y, a continuación, concederles acceso al rol SqlJDBCXAUser mientras esté conectado a la base de datos maestra.  
  
## <a name="example"></a>Ejemplo  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class testXA {  
  
   public static void main(String[] args) throws Exception {  
  
      // Create variables for the connection string.  
      String prefix = "jdbc:sqlserver://";  
      String serverName = "localhost";  
      int portNumber = 1433;  
      String databaseName = "AdventureWorks";   
      String user = "UserName";   
      String password = "*****";  
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
   XidImpl(int formatId, byte[] gtrid, byte[] bqual) {  
      this.formatId = formatId;  
      this.gtrid = gtrid;  
      this.bqual = bqual;  
   }  
  
   public String toString() {  
      int hexVal;  
      StringBuffer sb = new StringBuffer(512);  
      sb.append("formatId=" + formatId);  
      sb.append(" gtrid(" + gtrid.length + ")={0x");  
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
