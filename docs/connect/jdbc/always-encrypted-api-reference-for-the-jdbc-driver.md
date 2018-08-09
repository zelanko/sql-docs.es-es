---
title: Referencia de la API de Always Encrypted para JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b305c9e42f1eb7dffec8bd00204723a142a6b2e
ms.sourcegitcommit: 50144371c9ee924e5c0b4b9d3d4860f531c27426
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39582171"
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
|Nuevos métodos:<br /><br /> setColumnEncryptionTrustedMasterKeyPaths de void estático público (Map < String, lista\<cadena >> trustedKeyPaths)<br /><br /> updateColumnEncryptionTrustedMasterKeyPaths de void estático público (servidor de la cadena, lista\<cadena > trustedKeyPaths)<br /><br /> removeColumnEncryptionTrustedMasterKeyPaths void estático público (servidor de cadena)|Permite establecer, actualizar o quitar una lista de rutas de acceso de confianza a la clave para un servidor de base de datos. Si durante el procesamiento de una consulta de aplicación el controlador recibe una ruta de acceso a la clave que no figura en la lista, se producirá un error en la consulta. Esta propiedad proporciona protección adicional frente a los ataques de seguridad que implican un servidor SQL Server comprometido que envía rutas de acceso a la clave falsas que pueden provocar la divulgación de las credenciales del almacén de claves.|  
|Nuevo método:<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|Devuelve una lista de rutas de acceso a la clave de confianza para un servidor de base de datos.|  
|Nuevo método:<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)|Permite registrar los proveedores del almacén de claves personalizados. Se trata de un diccionario que asigna nombres de proveedor del almacén de claves para las implementaciones de proveedor del almacén de claves.<br /><br /> Para usar el almacén de claves de JVM, se debe crear una instancia de un objeto SQLServerColumnEncryptionJVMKeyStoreProvider con credenciales de almacén de claves de JVM y registrarlo en el controlador. El nombre de este proveedor debe ser "MSSQL_JVM_KEYSTORE".<br /><br /> Para usar el almacén de Azure Key Vault, deberá crear una instancia de un objeto SQLServerColumnEncryptionAzureKeyStoreProvider y registrarlo con el controlador. El nombre de este proveedor debe ser 'AZURE_KEY_VAULT'.|
|public final boolean getSendTimeAsDatetime()|Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|setSendTimeAsDatetime void público (sendTimeAsDateTimeValue booleano)|Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|

 **Clase SQLServerConnectionPoolProxy**
|Nombre|Descripción|  
|----------|-----------------|  
|public final boolean getSendTimeAsDatetime()|Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|setSendTimeAsDatetime void público (sendTimeAsDateTimeValue booleano)|Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|
     
  
 **Clase SQLServerDataSource**  
  
|Nombre|Descripción|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|Habilita o deshabilita la funcionalidad Always Encrypted para el objeto de origen de datos.<br /><br /> El valor predeterminado es Disabled.|  
|getColumnEncryptionSetting() de cadena pública|Recupera el valor de la funcionalidad Always Encrypted para el objeto de origen de datos.|
|setKeyStoreAuthentication void público (cadena keyStoreAuthentication)|Establece el nombre que identifica un almacén de claves. Solo el valor admitido es el **JavaKeyStorePassword** para identificar el Store de la clave de Java.<br/><br/>El valor predeterminado es null.|
|getKeyStoreAuthentication() de cadena pública|Obtiene el valor de la configuración de keyStoreAuthentication para el objeto de origen de datos.|
|setKeyStoreSecret void público (cadena keyStoreSecret)|Establece la contraseña del almacén de claves de Java. La contraseña para el almacén de claves y la clave debe ser el mismo. Tenga en cuenta que keyStoreAuthentication debe establecerse con **JavaKeyStorePassword**.|
|setKeyStoreLocation void público (cadena keyStoreLocation)|Establece la ubicación como el nombre de archivo del almacén de claves de Java. Tenga en cuenta que keyStoreAuthentication debe establecerse con **JavaKeyStorePassword**.|
|getKeyStoreLocation() de cadena pública|Recupera el keyStoreLocation para el Store de la clave de Java.|
  
 **Clase SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 La implementación del proveedor del almacén de claves del almacén de claves de Java. Esta clase permite usar certificados almacenados en el almacén de claves de Java como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerColumnEncryptionJavaKeyStoreProvider pública (keyStoreLocation String, char [] keyStoreSecret)|Proveedor de almacén de claves para el Store de la clave de Java.|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|Descifra el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante el certificado con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso a la clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (String, String, Byte[]).)|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)|Cifra una clave de cifrado de columna mediante el certificado con la ruta de acceso a la clave especificada y con el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso a la clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (String, String, Byte[]).)|  
|setName void público (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|public String getName ()|Obtiene el nombre de este proveedor de almacén de claves.|
  
 **Clase SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 La implementación del proveedor del almacén de claves para Azure Key Vault. Esta clase permite usar claves almacenadas en Azure Key Vault como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerColumnEncryptionAzureKeyVaultProvider pública (clientId de cadena, cadena clientKey)|Proveedor de almacén de claves para Azure Key Vault.  Deberá proporcionar el identificador y la clave del cliente solicita el token para autenticarse en Azure Key Vault.|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
| public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey) | Decryptes una clave de cifrado de columna cifrada (CEK). Este descifrado se realiza con un algoritmo de cifrado de RSA que se utiliza la clave asimétrica especificada por la ruta de acceso de la clave maestra.<br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (String, String, Byte[]).) |  
| public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey) | Cifra una clave de cifrado de columna, proporcionando la clave maestra de columna especificada para el algoritmo especificado.<br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (String, String, Byte[]).) |  
|setName void público (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|public String getName ()|Obtiene el nombre de este proveedor de almacén de claves.|  
  
  
 **Interfaz SQLServerKeyVaultAuthenticationCallback**  
  
 Esta interfaz contiene un método para la autenticación de Azure Key Vault, que consiste en ser implementada por el usuario.  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|getAccessToken de cadena pública (autoridad de cadena, recurso de cadena, cadena ámbito);|El método debe invalidarse. El método se utiliza para obtener acceso el token a Azure Key Vault.|  
  
 **Clase SQLServerColumnEncryptionKeyStoreProvider**  
  
 Amplíe esta clase para implementar un proveedor del almacén de claves personalizado.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Clase base para todos los proveedores del almacén de claves. Un proveedor personalizado debe derivarse de esta clase e invalidar sus funciones miembro. Luego, se debe registrar mediante SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Método de clase base para descifrar el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante la clave maestra de columna con la ruta de acceso a la clave especificada y el algoritmo especificado.|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|Método de clase base para cifrar una clave de cifrado de columna mediante la clave maestra de columna con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.|
|setName void abstracta pública (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|getName() de cadena abstracta pública|Obtiene el nombre de este proveedor de almacén de claves.|  
  
 Métodos nuevos o sobrecargados en **SQLServerPreparedStatement** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|setBigDecimal void público (int parameterIndex, BigDecimal x int precisión, escala int)<br /><br /> public void setObject (int parameterIndex, objeto x, targetSqlType int, precisión de entero, escala de int)<br /><br /> public void setObject (int parameterIndex, objeto x, SQLType targetSqlType, precisión de entero, escala de entero)<br /><br /> public void setTime (parameterIndex int, java.sql.Time x escala int)<br /><br /> public void setTimestamp (parameterIndex int, java.sql.Timestamp x escala int) <br />public void setDateTimeOffset (parameterIndex int, microsoft.sql.DateTimeOffset x escala int)|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren una precisión y la información de escala.|  
|setMoney void público (int parameterIndex, BigDecimal x)<br /><br /> setSmallMoney void público (int parameterIndex, BigDecimal x)<br /><br /> public void setUniqueIdentifier (int parameterIndex, guid de cadena)<br /><br /> setDateTime void público (parameterIndex int, java.sql.Timestamp x)<br /><br /> setSmallDateTime void público (parameterIndex int, java.sql.Timestamp x)|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método setTimestamp() existente se usa para enviar los valores de parámetro a la columna cifrada datetime2. Para los cifrados de datetime y smalldatetime columnas usar respectivamente los nuevos setDateTime() métodos y setSmallDateTime().|  
|final setBigDecimal void público (int parameterIndex, BigDecimal x int precisión, escala de int, boolean forceEncrypt)<br /><br /> pública setMoney void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> pública setSmallMoney void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> final setBoolean void público (parameterIndex int, boolean x, forceEncrypt booleano)<br /><br /> final setByte void público (parameterIndex int, byte x forceEncrypt booleano)<br /><br /> final setBytes void público (parameterIndex int, byte x[], forceEncrypt booleano)<br /><br /> final setUniqueIdentifier void público (int parameterIndex, guid de cadena, booleano forceEncrypt)<br /><br /> final setDouble void público (parameterIndex int, double x, forceEncrypt booleano)<br /><br /> final setFloat void público (parameterIndex int, float x, forceEncrypt booleano)<br /><br /> final setInt void público (parameterIndex int, valor de tipo int, boolean forceEncrypt)<br /><br /> final setLong void público (parameterIndex int, long x, forceEncrypt booleano)<br /><br /> pública final setObject (int parameterIndex, objeto x, targetSqlType int, precisión entero, escala de int, boolean forceEncrypt)<br /><br /> final setObject void público (parameterIndex int, objeto x, SQLType targetSqlType, precisión de entero, escala de entero, booleano forceEncrypt)<br /><br /> final setShort void público (parameterIndex int, short x, forceEncrypt booleano)<br /><br /> setString void final pública (int parameterIndex, str de cadena, booleano forceEncrypt)<br /><br /> final setNString void público (parameterIndex int, el valor de cadena, booleano forceEncrypt)<br /><br /> pública setTime void final (parameterIndex int, java.sql.Time x, escala de int, boolean forceEncrypt)<br /><br /> pública setTimestamp void final (parameterIndex int, java.sql.Timestamp, int escala x, forceEncrypt booleano)<br /><br /> pública setDateTimeOffset void final (parameterIndex int, microsoft.sql.DateTimeOffset x, escala de int, boolean forceEncrypt)<br /><br /> final setDateTime void público (parameterIndex int, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> final setSmallDateTime void público (parameterIndex int, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> pública setDate void final (parameterIndex int, java.sql.Date x java.util.Calendar cal, forceEncrypt booleano)<br /><br /> pública setTime void final (parameterIndex int, java.sql.Time x java.util.Calendar cal, forceEncrypt booleano)<br /><br /> pública setTimestamp void final (parameterIndex int, java.sql.Timestamp x java.util.Calendar cal, forceEncrypt booleano)|Establece el parámetro designado en el valor de Java indicado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|  
  
 Métodos nuevos o sobrecargados en **SQLServerCallableStatement** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)<br />public void setBigDecimal (cadena parameterName, BigDecimal bd, int precisión, escala int)<br /><br /> public void setTime (parameterName String, t java.sql.Time, escala de int)<br /><br /> public void setTimestamp (cadena parameterName, t java.sql.Timestamp, int escala)<br /><br /> public void setDateTimeOffset (parameterName String, microsoft.sql.DateTimeOffset t, escala int)<br/><br/>final setObject void público (sCol de cadena, objeto x, targetSqlType int, precisión de entero, escala de int)|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren una precisión y la información de escala.|  
|setDateTime void público (cadena parameterName, java.sql.Timestamp x)<br /><br /> setSmallDateTime void público (cadena parameterName, java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier (parameterName String, guid de cadena)<br /><br /> public void setMoney (cadena parameterName, BigDecimal bd)<br /><br /> public void setSmallMoney (cadena parameterName, BigDecimal bd)<br/><br/>getDateTime pública de marca de tiempo (int index)<br/><br/>getDateTime pública de marca de tiempo (cadena sCol)<br/><br/>pública getDateTime de marca de tiempo (el índice de int, el calendario cal)<br/><br/>getSmallDateTime pública de marca de tiempo (int index)<br/><br/>getSmallDateTime pública de marca de tiempo (cadena sCol)<br/><br/>pública getSmallDateTime de marca de tiempo (el índice de int, el calendario cal)<br/><br/>pública getSmallDateTime de marca de tiempo (nombre de la cadena, las cal de calendario)<br/><br/>pública BigDecimal getMoney (int index)<br/><br/>pública BigDecimal getMoney (cadena sCol)<br/><br/>pública BigDecimal getSmallMoney (int index)<br/><br/>pública BigDecimal getSmallMoney (cadena sCol)|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método setTimestamp() existente se usa para enviar los valores de parámetro a la columna cifrada datetime2. Para los cifrados de datetime y smalldatetime columnas usar respectivamente los nuevos setDateTime() métodos y setSmallDateTime().|  
|public void setObject (parameterName de cadena, objeto o, n int, int m, forceEncrypt booleano)<br /><br /> public void setObject (parameterName de cadena, objeto obj, SQLType jdbcType, escala de int, forceEncrypt booleano)<br /><br /> setDate void público (cadena parameterName, java.sql.Date x c de calendario, forceEncrypt booleano)<br /><br /> public void setTime (cadena parameterName, java.sql.Time t, escala int, boolean forceEncrypt)<br /><br /> setTime void público (cadena parameterName, java.sql.Time x c de calendario, forceEncrypt booleano)<br /><br /> public void setDateTime (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setDateTimeOffset (cadena parameterName, microsoft.sql.DateTimeOffset t, escala int, boolean forceEncrypt)<br /><br /> public void setSmallDateTime (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setTimestamp (cadena parameterName, t java.sql.Timestamp, int escala, forceEncrypt booleano)<br /><br /> public void setTimestamp (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setUniqueIdentifier (cadena parameterName, guid de cadena, booleano forceEncrypt)<br /><br /> public void setBytes (parameterName String, byte [] b, forceEncrypt booleano)<br /><br /> public void setByte (parameterName String, byte b, forceEncrypt booleano)<br /><br /> public void setString (parameterName de cadena, cadena s, forceEncrypt booleano)<br /><br /> final setNString void público (parameterName de cadena, valor de cadena, booleano forceEncrypt)<br /><br /> public void setMoney (cadena parameterName, BigDecimal bd, forceEncrypt booleano)<br /><br /> public void setSmallMoney (cadena parameterName, BigDecimal bd, forceEncrypt booleano)<br /><br /> public void setBigDecimal (cadena parameterName, BigDecimal bd, int precisión, escala de int, forceEncrypt booleano)<br /><br /> public void setDouble (parameterName de cadena, doble d, forceEncrypt booleano)<br /><br /> public void setFloat (parameterName String, float f, forceEncrypt booleano)<br /><br /> setInt void público (parameterName String, int i, forceEncrypt booleano)<br /><br /> public void setLong (parameterName String, long l, forceEncrypt booleano)<br /><br /> public void setShort (cadena parameterName, short s, forceEncrypt booleano)<br /><br /> public void setBoolean (parameterNames de cadena, booleano b, forceEncrypt booleano)<br/><br/>setTimeStamp void público (cadena sCol, java.sql.Timestamp x c de calendario, forceEncrypt booleano)|Establece el parámetro designado en el valor de Java indicado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|
 

 Métodos nuevos o sobrecargados en **SQLServerResultSet** clase  
  
|Nombre|Descripción|  
|----------|-----------------|  
|Public String getUniqueIdentifier (columnIndex int)<br/><br/>Public String getUniqueIdentifier (cadena columnLabel)<br/><br/>   java.sql.Timestamp pública getDateTime (columnIndex int) <br/><br/> java.sql.Timestamp pública getDateTime (columnName cadena)   <br/><br/> java.sql.Timestamp pública getDateTime (int columnIndex, calendario cal)   <br/><br/>java.sql.Timestamp pública getDateTime (cadena colName, calendario cal)    <br/><br/>getSmallDateTime java.sql.Timestamp pública (columnIndex int)    <br/><br/> getSmallDateTime java.sql.Timestamp pública (columnName cadena)   <br/><br/> java.sql.Timestamp pública getSmallDateTime (int columnIndex, calendario cal)   <br/><br/> java.sql.Timestamp pública getSmallDateTime (cadena colName, calendario cal)   <br/><br/>  pública BigDecimal getMoney (columnIndex int)  <br/><br/> pública BigDecimal getMoney (columnName cadena)   <br/><br/> pública BigDecimal getSmallMoney (columnIndex int)   <br/><br/>  pública BigDecimal getSmallMoney (columnName cadena)  <br/><br/>updateMoney void público (cadena columnName, BigDecimal x)    <br/><br/>  updateSmallMoney void público (cadena columnName, BigDecimal x)  <br/><br/>     updateDateTime void público (índice de int, java.sql.Timestamp x) <br/><br/> updateSmallDateTime void público (índice de int, java.sql.Timestamp x) |Estos métodos se agregan para admitir Always Encrypted para tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método updateTimestamp() existente se usa para actualizar las columnas datetime2 cifrados. Para los cifrados de datetime y smalldatetime columnas usar respectivamente los nuevos updateDateTime() métodos y updateSmallDateTime().|
|public void updateBoolean (índice int, boolean x, forceEncrypt booleano)  <br/><br/>  public void updateByte (índice de int, byte x forceEncrypt booleano)  <br/><br/>  public void updateShort (índice int, short x, forceEncrypt booleano)  <br/><br/> public void updateInt (índice de int, int x forceEncrypt booleano)   <br/><br/>  public void updateLong (índice de int, long x, forceEncrypt booleano)  <br/><br/> public void updateFloat (índice de int, float x, forceEncrypt booleano)   <br/><br/> public void updateDouble (int index, double x, forceEncrypt booleano)   <br/><br/> updateMoney void público (int index, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateMoney void público (cadena columnName, BigDecimal x forceEncrypt booleano)  <br/><br/> updateSmallMoney void público (int index, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateSmallMoney void público (cadena columnName, BigDecimal x forceEncrypt booleano)  <br/><br/> public void updateBigDecimal (int index, BigDecimal x precisión entero, escala de entero, booleano forceEncrypt)   <br/><br/>  public void updateString (int columnIndex, stringValue de cadena, booleano forceEncrypt)  <br/><br/>  public void updateNString (int columnIndex, Nopción de cadena, booleano forceEncrypt)  <br/><br/>  public void updateNString (columnLabel de cadena, cadena Nopción, forceEncrypt booleano)  <br/><br/> public void updateBytes (índice int, byte x[], forceEncrypt booleano)   <br/><br/>  public void updateDate (índice de int, java.sql.Date x forceEncrypt booleano)  <br/><br/> updateTime void público (índice de int, java.sql.Time x, escala de entero, booleano forceEncrypt)   <br/><br/> updateTimestamp void público (índice de int, java.sql.Timestamp, int escala x, forceEncrypt booleano)   <br/><br/> updateDateTime void público (índice de int, java.sql.Timestamp x, escala de entero, booleano forceEncrypt)   <br/><br/> updateSmallDateTime void público (índice de int, java.sql.Timestamp x, escala de entero, booleano forceEncrypt)   <br/><br/>  updateDateTimeOffset void público (índice de int, microsoft.sql.DateTimeOffset x, escala de entero, booleano forceEncrypt)  <br/><br/> updateUniqueIdentifier void público (índice de int, String x forceEncrypt booleano)    <br/><br/>  public void updateObject (int index, objeto x, int precisión, escala de int, boolean forceEncrypt)  <br/><br/>  public void updateObject (int index, objeto obj, SQLType targetSqlType, int escala, forceEncrypt booleano)  <br/><br/> public void updateBoolean (columnName de cadena, booleano x, forceEncrypt booleano)    <br/><br/>  public void updateByte (columnName String, byte x forceEncrypt booleano)  <br/><br/>  public void updateShort (cadena columnName, x corto, forceEncrypt booleano)  <br/><br/> public void updateInt (columnName String, int x forceEncrypt booleano)   <br/><br/>   public void updateLong (columnName String, long x, forceEncrypt booleano) <br/><br/>  public void updateFloat (columnName String, float x, forceEncrypt booleano)  <br/><br/>  public void updateDouble (columnName de cadena, doble x, forceEncrypt booleano)  <br/><br/> updateBigDecimal void público (cadena columnName, BigDecimal x forceEncrypt booleano)   <br/><br/>  public void updateBigDecimal (cadena columnName, BigDecimal x precisión entero, escala de entero, booleano forceEncrypt)  <br/><br/> updateString void público (columnName de cadena, cadena x forceEncrypt booleano)   <br/><br/>  public void updateBytes (cadena columnName, x[] bytes, forceEncrypt booleano)  <br/><br/> public void updateDate (cadena columnName, java.sql.Date x forceEncrypt booleano)   <br/><br/>  updateTime void público (cadena columnName, java.sql.Time x, escala de int, boolean forceEncrypt)  <br/><br/>  updateTimestamp void público (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)  <br/><br/> updateDateTime void público (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)   <br/><br/>  updateSmallDateTime void público (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)  <br/><br/>  updateDateTimeOffset void público (columnName String, microsoft.sql.DateTimeOffset x, escala de int, boolean forceEncrypt)  <br/><br/>  updateUniqueIdentifier void público (columnName de cadena, cadena x forceEncrypt booleano)<br/><br/>public void updateObject (columnName de cadena, objeto x, int precisión, escala de int, boolean forceEncrypt)<br/><br/>pública void updateObject (columnName de cadena, objeto obj, SQLType targetSqlType, escala de int, forceEncrypt booleano)|Actualice la columna designada con el valor de java especificado.<br/><br/>Si el forceEncrypt booleano se establece en true, la columna solo se establecerá si se cifra y Always Encrypted está habilitado en la conexión o en la instrucción.<br/><br/>Si el forceEncrypt booleano se establece en false, el controlador no forzar el cifrado en los parámetros.|

  
Nuevos tipos en **microsoft.sql.Types** clase
|Nombre|Descripción|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Usar estos tipos como los tipos de SQL de destino al enviar valores de parámetro **cifrados** datetime, smalldatetime, money, smallmoney, columnas uniqueidentifier con métodos setObject()/updateObject() API.|  
  
  
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
|pública createStatement de instrucción (nLas int, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto de instrucción que genera objetos ResultSet con el tipo especificado, simultaneidad, capacidad de alojamiento y configuración de cifrado de columna.|  
|pública prepareCall de CallableStatement (cadena sql, nLas int, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|Crea un objeto CallableStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con el tipo especificado, la simultaneidad y capacidad de alojamiento.|  
|prepareStatement de PreparedStatement pública (sql String, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto PreparedStatement con la configuración de cifrado de columna especificada que tiene la capacidad de recuperar claves generadas automáticamente.|  
|prepareStatement de PreparedStatement pública (cadena sql, cadena [] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con los nombres de columna especificado.|  
|prepareStatement de PreparedStatement pública (sql String, int [] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con los índices de columna especificado.|  
|prepareStatement de PreparedStatement pública (cadena sql, nLas int, nConcur int, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto PreparedStatement con la configuración de cifrado de columna determinada que genere objetos ResultSet con el tipo especificado, la simultaneidad y capacidad de alojamiento.|  
  
> [!NOTE]  
>  Si Always Encrypted está deshabilitado para una consulta y la consulta tiene parámetros que deben estar cifrados (los parámetros que corresponden a columnas cifradas), se producirá un error en la consulta.  
>   
>  Si Always Encrypted está deshabilitado para una consulta y la consulta devuelve los resultados de las columnas cifradas, la consulta devolverá valores cifrados. Los valores cifrados tendrán el tipo de datos varbinary.  
  
 ## <a name="see-also"></a>Ver también  
 [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

