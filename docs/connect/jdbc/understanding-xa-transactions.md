---
title: Descripción de las transacciones XA
description: Microsoft JDBC Driver para SQL Server es compatible con las transacciones distribuidas opcionales de Java Platform, Enterprise Edition/JDBC 2.0.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bcf55fd300c977105229473228955581da7cdd3
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528739"
---
# <a name="understanding-xa-transactions"></a>Descripción de las transacciones XA

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] es compatible con las transacciones distribuidas opcionales de Java Platform, Enterprise Edition/JDBC 2.0. Las conexiones JDBC obtenidas de la clase [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) pueden participar en entornos estándar de procesamiento de transacciones distribuidas, como los servidores de aplicaciones de Java Platform, Enterprise Edition (Java EE).  

En este artículo, XA representa la arquitectura extendida.

> [!WARNING]  
> Microsoft JDBC Driver 4.2 (y superior) para SQL incluye nuevas opciones de tiempo de espera para la característica de reversión automática existente de transacciones no preparadas. Consulte [Configurar el valor de tiempo de espera del servidor para la reversión automática de transacciones no preparadas](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide) más adelante en este tema para obtener más información.  

## <a name="remarks"></a>Observaciones

Las clases para la implementación de las transacciones distribuidas son las siguientes:  
  
| Clase                                              | Implementaciones                      | Descripción                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | La fábrica de clases para conexiones distribuidas.    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | El adaptador de recursos para el administrador de transacciones. |
  
> [!NOTE]  
> Las conexiones de transacciones distribuidas XA se establecen de forma predeterminada en el nivel de aislamiento Read Committed.  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>Instrucciones y limitaciones al usar transacciones XA  

Las siguientes instrucciones adicionales se aplican a las transacciones fuertemente acopladas:  

- Cuando utiliza transacciones XA junto con MS DTC, puede observar que la versión actual de Microsoft DTC (Coordinador de transacciones distribuidas) no admite el comportamiento de bifurcación XA estrechamente acoplado. Por ejemplo, MS DTC tiene una asignación unívoca entre un identificador de rama de transacción XA (XID) y un identificador de transacción de MS DTC, y el trabajo que realizan las bifurcaciones XA débilmente acopladas se aísla entre estas.  
  
- MS DTC admite también las ramas XA estrechamente ligadas donde varias ramas XA con el mismo identificador de transacción global (GTRID) se asignan a un único identificador de transacción de MS DTC. Esta compatibilidad permite que varias ramas XA estrechamente ligadas vean los cambios respectivos en el administrador de recursos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Una marca [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) permite que las aplicaciones usen transacciones XA estrechamente ligadas, que tienen identificadores de rama de transacción XA diferentes (BQUAL), pero el mismo identificador de transacción global (GTRID) e identificador de formato (FormatID). Para utilizar esa característica, debe establecer [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) en el parámetro de marcas del método XAResource.start:
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>Instrucciones de configuración

Los siguientes pasos son necesarios si desea usar los orígenes de datos XA junto con Microsoft DTC (Coordinador de transacciones distribuidas) para administrar las transacciones distribuidas.  

> [!NOTE]  
> Los componentes de transacciones distribuidas de JDBC están incluidos en el directorio xa de la instalación del controlador JDBC. Estos componentes incluyen los archivos xa_install.sql y sqljdbc_xa.dll.  

> [!NOTE]  
> A partir de la versión preliminar pública CTP 2.0 de SQL Server 2019, los componentes de transacciones distribuidas de JDBC XA se incluyen en el motor de SQL Server y se pueden habilitar o deshabilitar con un procedimiento almacenado del sistema.
> Para permitir que los componentes necesarios realicen transacciones distribuidas de XA con el controlador JDBC, ejecute el siguiente procedimiento almacenado.
>
> EXEC sp_sqljdbc_xa_install
>
> Para deshabilitar los componentes instalados previamente, ejecute el siguiente procedimiento almacenado.
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>Ejecutar el servicio MS DTC

El servicio MS DTC debe estar marcado como **Automático** en Service Manager para asegurarse de que se esté ejecutando cuando se inicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para habilitar Microsoft DTC (Coordinador de transacciones distribuidas) para las transacciones XA, debe seguir estos pasos:  
  
En Windows Vista y versiones posteriores:  
  
1. Haga clic en **Inicio**, escriba **dcomcnfg** en el cuadro **Iniciar búsqueda** y presione ENTRAR para abrir **Servicios de componentes**. También puede escribir %windir%\system32\comexp.msc en el cuadro **Iniciar búsqueda** para abrir **Servicios de componentes**.  
  
2. Expanda Servicios de componentes, Equipos, Mi PC y Microsoft DTC (Coordinador de transacciones distribuidas).  
  
3. Haga clic con el botón derecho en **DTC local** y seleccione **Propiedades**.  
  
4. En el cuadro de diálogo **Propiedades de DTC local**, haga clic en la pestaña **Seguridad**.  
  
5. Active la casilla **Habilitar transacciones XA** y haga clic en **Aceptar**. De este modo, se reiniciará el servicio MS DTC.
  
6. Vuelva a hacer clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** y luego cierre **Servicios de componentes**.  
  
7. Detenga y reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para asegurarse de que se sincroniza con los cambios realizados en MS DTC.  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>Configurar los componentes de transacciones distribuidas de JDBC  

Puede configurar los componentes de transacciones distribuidas del controlador JDBC mediante estos pasos:  
  
1. Copie el nuevo archivo sqljdbc_xa.dll del directorio de instalación del controlador JDBC al directorio Binn de cada equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que vaya a participar en las transacciones distribuidas.  
  
    > [!NOTE]  
    > Si usa transacciones XA con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, use el archivo sqljdbc_xa.dll de la carpeta x86, aunque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esté instalado en un procesador x64. Si usa transacciones XA con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits en el procesador x64, use el archivo sqljdbc_xa.dll de la carpeta x64.  
  
2. Ejecute el script de base de datos xa_install.sql en cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que participe en las transacciones distribuidas. Este script instala los procedimientos almacenados extendidos que son llamados por sqljdbc_xa.dll. Estos procedimientos almacenados extendidos implementan la compatibilidad con transacciones distribuidas y XA para [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. Debe ejecutar este script como administrador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3. Para conceder permisos a un usuario concreto de modo que pueda participar en las transacciones distribuidas con el controlador JDBC, agregue el usuario al rol SqlJDBCXAUser.  
  
Solo puede configurar una versión del ensamblado sqljdbc_xa.dll en cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada vez. Las aplicaciones pueden necesitar diferentes versiones del controlador JDBC para conectar con la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la conexión XA. En ese caso, sqljdbc_xa.dll, que se incluye en el controlador JDBC más reciente, debe instalarse en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Hay tres maneras de comprobar la versión de sqljdbc_xa.dll instalada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:
  
1. Abra el directorio LOG del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a participar en las transacciones distribuidas. Seleccione y abra el archivo "ERRORLOG" de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Busque la frase "Using 'SQLJDBC_XA.dll' version..." en el archivo "ERRORLOG".  
  
2. Abra el directorio Binn del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a participar en las transacciones distribuidas. Seleccione el ensamblado sqljdbc_xa.dll.

    - En Windows Vista o versiones posteriores: Haga clic con el botón derecho en sqljdbc_xa.dll y después seleccione Propiedades. Después, haga clic en la pestaña **Detalles**. En el campo **Versión del archivo** se muestra qué versión de sqljdbc_xa.dll está actualmente instalada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3. Configure la funcionalidad de registro tal como se muestra en el ejemplo de código de la sección siguiente. Busque la frase "Server XA DLL version:..." en el archivo de registro de resultados.  

### <a name="configuring-server-side-timeout-settings-for-automatic-rollback-of-unprepared-transactions"></a><a name="BKMK_ServerSide"></a> Configurar el valor de tiempo de espera del servidor para la reversión automática de transacciones no preparadas  

> [!WARNING]  
> Esta opción de servidor es nueva en Microsoft JDBC Driver 4.2 (y superior) para SQL Server. Para obtener el comportamiento actualizado, asegúrese de que se ha actualizado sqljdbc_xa.dll en el servidor. Para más información sobre cómo establecer los tiempos de espera del cliente, vea [XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html).  

Hay dos configuraciones de registro (valores DWORD) para controlar el comportamiento de tiempo de espera de las transacciones distribuidas:  
  
- **XADefaultTimeout** (en segundos): El valor de tiempo de espera predeterminado que se usará cuando el usuario no especifique ningún tiempo de espera. El valor predeterminado es 0.  
  
- **XAMaxTimeout** (en segundos): El valor máximo de tiempo de espera que el usuario puede establecer. El valor predeterminado es 0.  
  
Estos valores son específicos de la instancia de SQL Server y se deben crear en la siguiente clave del registro:  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> Si una instancia de SQL Server de 32 bits se ejecuta en un equipo de 64 bits, se debe crear la configuración del Registro bajo la siguiente clave: `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
Cuando se inicia, se establece un valor de tiempo de espera para cada transacción y el SQL Server revierte la transacción si expira el tiempo de espera. El tiempo de espera se determina en función de esta configuración del registro y de lo que el usuario haya especificado a través de XAResource.setTransactionTimeout(). A continuación se muestran algunos ejemplos de cómo se interpretan estos valores de tiempo de espera:  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`
  
     Significa que no se usará ningún tiempo de espera predeterminado y tampoco se exigirá que los clientes establezcan un tiempo de espera máximo. En este caso, las transacciones tendrán un tiempo de espera solo si el cliente establece un tiempo de espera mediante XAResource.setTransactionTimeout.  
  
- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`
  
     Significa que todas las transacciones tendrán un tiempo de espera de 60 segundos si el cliente no especifica ningún tiempo de espera. Si el cliente especifica un tiempo de espera, entonces se usará ese valor de tiempo de espera. No se exige ningún valor máximo para el tiempo de espera.  
  
- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`
  
     Significa que todas las transacciones tendrán un tiempo de espera de 30 segundos si el cliente no especifica ningún tiempo de espera. Si el cliente especifica algún tiempo de espera, entonces se usará el tiempo de espera del cliente siempre y cuando sea inferior a 60 segundos (el valor máximo).  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`
  
     Significa que todas las transacciones tendrán un tiempo de espera de 30 segundos (el valor máximo) si el cliente no especifica ningún tiempo de espera. Si el cliente especifica algún tiempo de espera, entonces se usará el tiempo de espera del cliente siempre y cuando sea inferior a 30 segundos (el valor máximo).  
  
### <a name="upgrading-sqljdbc_xadll"></a>Actualización de sqljdbc_xa.dll

Al instalar una nueva versión del controlador JDBC, también debe usar sqljdbc_xa.dll de la nueva versión para actualizar sqljdbc_xa.dll en el servidor.  
  
> [!IMPORTANT]  
> Debe actualizar sqljdbc_xa.dll durante un intervalo de mantenimiento o cuando no haya transacciones MS DTC en curso.
  
1. Descargue sqljdbc_xa.dll con el comando de [!INCLUDE[tsql](../../includes/tsql-md.md)] **DBCC sqljdbc_xa (FREE)** .  
  
2. Copie el nuevo archivo sqljdbc_xa.dll del directorio de instalación del controlador JDBC al directorio Binn de cada equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que vaya a participar en las transacciones distribuidas.  
  
    La nueva DLL se cargará cuando se llame a un procedimiento extendido en sqljdbc_xa.dll. No necesita reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cargar las nuevas definiciones.  
  
### <a name="configuring-the-user-defined-roles"></a>Configurar los roles definidos por el usuario

Para conceder permisos a un usuario concreto de modo que pueda participar en las transacciones distribuidas con el controlador JDBC, agregue el usuario al rol SqlJDBCXAUser. Por ejemplo, use el siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] para agregar un usuario denominado "shelby" (usuario de inicio de sesión estándar de SQL denominado "shelby") al rol SqlJDBCXAUser:  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

Los roles definidos por el usuario de SQL se definen para cada base de datos. Para crear su propio rol por motivos de seguridad, debe definir el rol en cada base de datos y agregar los usuarios para cada base de datos. El rol SqlJDBCXAUser se define estrictamente en la base de datos maestra porque se utiliza para conceder acceso a los procedimientos almacenados extendidos del controlador JDBC de SQL que se encuentran en la base de datos maestra. En primer lugar, debe conceder acceso a cada usuario a la base de datos maestra y, a continuación, concederles acceso al rol SqlJDBCXAUser mientras esté conectado a la base de datos maestra.  

## <a name="example"></a>Ejemplo  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
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

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

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
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>Consulte también  

[Transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
