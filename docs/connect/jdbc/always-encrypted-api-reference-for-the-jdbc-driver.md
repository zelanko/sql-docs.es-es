---
title: Referencia de la API de Always Encrypted para JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66f659f5fbb2daa0b0a9969c3e7cde75dccc53d0
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361675"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Referencia de la API de Always Encrypted para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted permite a los clientes cifrar datos confidenciales en aplicaciones de cliente y nunca revelar las claves de cifrado en SQL Server. Un controlador habilitado para Always Encrypted instalado en el equipo cliente consigue esta funcionalidad al cifrar y descifrar automáticamente los datos confidenciales en la aplicación cliente de SQL Server. El controlador cifra los datos en columnas confidenciales antes de pasar los datos a SQL Server y vuelve a escribir las consultas automáticamente para que se conserve la semántica de la aplicación. De forma similar, el controlador descifra de forma transparente los datos almacenados en columnas de base de datos cifradas que se encuentran en los resultados de la consulta. Para obtener más información, consulte [Always Encrypted (motor de base de datos)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) y [uso de Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Always Encrypted solo se admite en Microsoft JDBC Driver 6.0 o superior para SQL Server con SQL Server 2016.  
  
 ## <a name="always-encrypted-api-references"></a>Referencias de la API de Always Encrypted
 
 Hay varias nuevas adiciones y modificaciones a la API de controlador JDBC que se pueden usar en aplicaciones cliente y que utilizan Always Encrypted.  
  
 **Clase SQLServerConnection**  
  
|Nombre|Descripción|  
|----------|-----------------|  
|Nueva palabra clave de cadena de conexión:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled habilita la funcionalidad Always Encrypted para la conexión ycolumnEncryptionSetting=Disabled la deshabilita. Los valores aceptados son Enabled y Disabled. El valor predeterminado es Disabled.|  
|Nuevos métodos:<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|Permite establecer, actualizar o quitar una lista de rutas de acceso de confianza a la clave para un servidor de base de datos. Si durante el procesamiento de una consulta de aplicación el controlador recibe una ruta de acceso a la clave que no figura en la lista, se producirá un error en la consulta. Esta propiedad proporciona protección adicional frente a los ataques de seguridad que implican un servidor SQL Server comprometido que envía rutas de acceso a la clave falsas que pueden provocar la divulgación de las credenciales del almacén de claves.|  
|Nuevo método:<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|Devuelve una lista de rutas de acceso a la clave de confianza para un servidor de base de datos.|  
|Nuevo método:<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|Permite registrar los proveedores del almacén de claves personalizados. Se trata de un diccionario que asigna nombres de proveedor del almacén de claves para las implementaciones de proveedor del almacén de claves.<br /><br /> Para usar el almacén de claves de JVM, se debe crear una instancia de un objeto SQLServerColumnEncryptionJVMKeyStoreProvider con credenciales de almacén de claves de JVM y registrarlo en el controlador. El nombre de este proveedor debe ser "MSSQL_JVM_KEYSTORE".<br /><br /> Para usar el almacén de Azure Key Vault, deberá crear una instancia de un objeto SQLServerColumnEncryptionAzureKeyStoreProvider y registrarlo con el controlador. El nombre de este proveedor debe ser 'AZURE_KEY_VAULT'.|
|`public final boolean getSendTimeAsDatetime()`|Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|

 **Clase SQLServerConnectionPoolProxy**
 
|Nombre|Descripción|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|
     
  
 **Clase SQLServerDataSource**  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|Habilita o deshabilita la funcionalidad Always Encrypted para el objeto de origen de datos.<br /><br /> El valor predeterminado es Disabled.|  
|`public String getColumnEncryptionSetting()`|Recupera el valor de la funcionalidad Always Encrypted para el objeto de origen de datos.|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|Establece el nombre que identifica un almacén de claves. Solo el valor admitido es el **JavaKeyStorePassword** para identificar el Store de la clave de Java.<br/><br/>El valor predeterminado es null.|
|`public String getKeyStoreAuthentication()`|Obtiene el valor de la configuración de keyStoreAuthentication para el objeto de origen de datos.|
|`public void setKeyStoreSecret(String keyStoreSecret)`|Establece la contraseña del almacén de claves de Java. La contraseña para el almacén de claves y la clave debe ser el mismo. Tenga en cuenta que keyStoreAuthentication debe establecerse con **JavaKeyStorePassword**.|
|`public void setKeyStoreLocation(String keyStoreLocation)`|Establece la ubicación como el nombre de archivo del almacén de claves de Java. Tenga en cuenta que keyStoreAuthentication debe establecerse con **JavaKeyStorePassword**.|
|`public String getKeyStoreLocation()`|Recupera el keyStoreLocation para el Store de la clave de Java.|
  
 **Clase SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 La implementación del proveedor del almacén de claves del almacén de claves de Java. Esta clase permite usar certificados almacenados en el almacén de claves de Java como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Proveedor de almacén de claves para el Store de la clave de Java.|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|Descifra el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante el certificado con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso a la clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|Cifra una clave de cifrado de columna mediante el certificado con la ruta de acceso a la clave especificada y con el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso a la clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).)|  
|`public void setName (String name)`|Establece el nombre de este proveedor de almacén de claves.|
|`public String getName ()`|Obtiene el nombre de este proveedor de almacén de claves.|
  
 **Clase SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 La implementación del proveedor del almacén de claves para Azure Key Vault. Esta clase permite usar claves almacenadas en Azure Key Vault como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Proveedor de almacén de claves para Azure Key Vault.  Deberá proporcionar el identificador y la clave del cliente solicita el token para autenticarse en Azure Key Vault.|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Decryptes una clave de cifrado de columna cifrada (CEK). Este descifrado se realiza con un algoritmo de cifrado de RSA que se utiliza la clave asimétrica especificada por la ruta de acceso de la clave maestra.<br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey(String, String, Byte[]).) |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | Cifra una clave de cifrado de columna, proporcionando la clave maestra de columna especificada para el algoritmo especificado.<br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey(String, String, Byte[]).) |  
|`public void setName (String name)`|Establece el nombre de este proveedor de almacén de claves.|
|`public String getName ()`|Obtiene el nombre de este proveedor de almacén de claves.|  
  
  
 **Interfaz SQLServerKeyVaultAuthenticationCallback**  
  
 Esta interfaz contiene un método para la autenticación de Azure Key Vault, que consiste en ser implementada por el usuario.  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|El método debe invalidarse. El método se utiliza para obtener acceso el token a Azure Key Vault.|  
  
 **Clase SQLServerColumnEncryptionKeyStoreProvider**  
  
 Amplíe esta clase para implementar un proveedor del almacén de claves personalizado.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Clase base para todos los proveedores del almacén de claves. Un proveedor personalizado debe derivarse de esta clase e invalidar sus funciones miembro. Luego, se debe registrar mediante SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|Método de clase base para descifrar el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante la clave maestra de columna con la ruta de acceso a la clave especificada y el algoritmo especificado.|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|Método de clase base para cifrar una clave de cifrado de columna mediante la clave maestra de columna con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.|
|`public abstract void setName(String name)`|Establece el nombre de este proveedor de almacén de claves.|
|`public abstract String getName()`|Obtiene el nombre de este proveedor de almacén de claves.|  
  
 Métodos nuevos o sobrecargados en **SQLServerPreparedStatement** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren una precisión y la información de escala.|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que la existente `setTimestamp()` método se utiliza para enviar los valores de parámetro a la columna cifrada datetime2. Para las columnas cifradas de datetime y smalldatetime, use los nuevos métodos `setDateTime()` y `setSmallDateTime()` respectivamente.|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|Establece el parámetro designado en el valor de Java indicado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|  
  
 Métodos nuevos o sobrecargados en **SQLServerCallableStatement** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren una precisión y la información de escala.|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que la existente `setTimestamp()` método se utiliza para enviar los valores de parámetro a la columna cifrada datetime2. Para las columnas cifradas de datetime y smalldatetime, use los nuevos métodos `setDateTime()` y `setSmallDateTime()` respectivamente.|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|Establece el parámetro designado en el valor de Java indicado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|
 

 Métodos nuevos o sobrecargados en **SQLServerResultSet** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |Estos métodos se agregan para admitir Always Encrypted para tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que la existente `updateTimestamp()` método se utiliza para actualizar las columnas datetime2 cifrados. Para las columnas cifradas de datetime y smalldatetime, use los nuevos métodos `updateDateTime()` y `updateSmallDateTime()` respectivamente.|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|Actualice la columna designada con el valor de java especificado.<br/><br/>Si el forceEncrypt booleano se establece en true, la columna solo se establecerá si se cifra y Always Encrypted está habilitado en la conexión o en la instrucción.<br/><br/>Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|

  
Nuevos tipos en **microsoft.sql.Types** clase

|Nombre|Descripción|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Usar estos tipos como los tipos de SQL de destino al enviar valores de parámetro **cifrados** datetime, smalldatetime, money, smallmoney, columnas uniqueidentifier mediante `setObject()/updateObject()` métodos de API.|  
  
  
 **SQLServerStatementColumnEncryptionSetting Enum**  
  
 Especifica cómo se enviarán los datos y cómo se recibe al leer y escribir las columnas cifradas. Según su consulta específica, impacto en el rendimiento puede reducirse omitiendo el controlador de Always Encrypted procesamiento cuando se usan columnas sin cifrar. Tenga en cuenta que esta configuración no se puede usar para omitir el cifrado y obtener acceso a datos de texto simple.  
  
 **Sintaxis**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Miembros**  
  
|Nombre|Descripción|  
|----------|-----------------|  
|UseConnectionSetting|Especifica que el comando de forma predeterminada la configuración de Always Encrypted en la cadena de conexión.|  
|Habilitado|Habilita siempre cifrado para la consulta.|  
|ResultSetOnly|Especifica que solo los resultados del comando deben procesarse por la rutina siempre cifrado en el controlador. Use este valor cuando el comando no tiene parámetros que requieren cifrado.|  
|Deshabilitado|Deshabilita siempre cifrado para la consulta.|  
  
 La configuración del nivel de instrucción para AE se agrega a la clase SQLServerConnection y a la clase SQLServerConnectionPoolProxy. Los siguientes métodos en estas clases están sobrecargados con la nueva configuración.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Crea un objeto de instrucción que genera objetos ResultSet con el tipo especificado, simultaneidad, capacidad de alojamiento y configuración de cifrado de columna.|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|Crea un objeto CallableStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con el tipo especificado, la simultaneidad y capacidad de alojamiento.|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Crea un objeto PreparedStatement con la configuración de cifrado de columna especificada que tiene la capacidad de recuperar claves generadas automáticamente.|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con los nombres de columna especificado.|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con los índices de columna especificado.|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con el tipo especificado, la simultaneidad y capacidad de alojamiento.|  
  
> [!NOTE]  
>  Si Always Encrypted está deshabilitado para una consulta y la consulta tiene parámetros que deben estar cifrados (los parámetros que corresponden a columnas cifradas), se producirá un error en la consulta.  
>   
>  Si Always Encrypted está deshabilitado para una consulta y la consulta devuelve los resultados de las columnas cifradas, la consulta devolverá valores cifrados. Los valores cifrados tendrán el tipo de datos varbinary.  
  
 ## <a name="see-also"></a>Consulte también  
 [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

