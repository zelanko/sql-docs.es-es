---
title: Always Encrypted referencia de API para el controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 951172d75cd37687482e1a6ce8ba4476872d2d4b
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Always Encrypted referencia de API para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted permite a los clientes cifrar datos confidenciales en aplicaciones de cliente y nunca revelar las claves de cifrado en SQL Server. Un controlador habilitado para Always Encrypted instalado en el equipo cliente consigue esto al cifrar y descifrar automáticamente los datos confidenciales en la aplicación cliente de SQL Server. El controlador cifra los datos en columnas confidenciales antes de pasar los datos a SQL Server y vuelve a escribir las consultas automáticamente para que se conserve la semántica de la aplicación. De forma similar, el controlador descifra de forma transparente los datos almacenados en columnas de base de datos cifradas que se incluyen en los resultados de la consulta. Para obtener más información, consulte [Always Encrypted (motor de base de datos)](/sql-docs/docs/relational-databases/security/encryption/always-encrypted-database-engine) y [usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  Always Encrypted es compatible con Microsoft JDBC Driver 6.0 o posterior para que SQL Server con SQL Server 2016.  
  
 Hay varias nuevas adiciones y modificaciones a la API de controlador JDBC que se pueden usar en aplicaciones cliente y que utilizan Always Encrypted.  
  
 **Clase SQLServerConnection**  
  
|Nombre|Descripción|  
|----------|-----------------|  
|Nueva palabra clave de cadena de conexión:<br /><br /> columnEncryptionSetting|columnEncryptionSetting = Enabled habilita la funcionalidad de Always Encrypted para la conexión y columnEncryptionSetting = Disabled la deshabilita. Los valores aceptados son Enabled y Disabled. El valor predeterminado es Disabled.|  
|Nuevos métodos:<br /><br /> setColumnEncryptionTrustedMasterKeyPaths de void estático público (mapa < cadena, se muestran\<cadena >> trustedKeyPaths)<br /><br /> updateColumnEncryptionTrustedMasterKeyPaths de void estático público (servidor de cadena, lista\<cadena > trustedKeyPaths)<br /><br /> removeColumnEncryptionTrustedMasterKeyPaths void estático público (servidor de cadena)|Permite conjunto/actualizar/quitar una lista de rutas de acceso de claves confianza para un servidor de base de datos. Si durante el procesamiento de una consulta de aplicación el controlador recibe una ruta de acceso a la clave que no figura en la lista, se producirá un error en la consulta. Esta propiedad proporciona protección adicional contra los ataques de seguridad que implican un servidor SQL Server comprometido que proporciona rutas de acceso a la clave falsas que pueden provocar la divulgación de las credenciales del almacén de claves.|  
|Nuevo método:<br /><br /> Mapa estático público < cadena, se muestran\<cadena >> getColumnEncryptionTrustedMasterKeyPaths()|Devuelve una lista de rutas de acceso a la clave de confianza para un servidor de base de datos.|  
|Nuevo método:<br /><br /> registerColumnEncryptionKeyStoreProviders de void estático público (mapa\<String, SQLServerColumnEncryptionKeyStoreProvider > clientKeyStoreProviders)|Permite registrar los proveedores del almacén de claves personalizados. Se trata de un diccionario que asigna nombres de proveedor del almacén de claves para las implementaciones de proveedor del almacén de claves.<br /><br /> Para usar el almacén de claves de JVM, se debe crear una instancia de un objeto SQLServerColumnEncryptionJVMKeyStoreProvider con credenciales de almacén de claves de JVM y registrarlo en el controlador. El nombre de este proveedor debe ser 'MSSQL_JVM_KEYSTORE'.<br /><br /> Para usar el almacén de almacén de claves de Azure necesario crear una instancia de un objeto SQLServerColumnEncryptionAzureKeyStoreProvider y registrarlo con el controlador. El nombre de este proveedor debe ser 'AZURE_KEY_VAULT'.|
|pública getSendTimeAsDatetime() booleano final|Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|setSendTimeAsDatetime void público (boolean sendTimeAsDateTimeValue)|Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|

 **Clase SQLServerConnectionPoolProxy**
|Nombre|Description|  
|----------|-----------------|  
|pública getSendTimeAsDatetime() booleano final|Devuelve el valor de la propiedad de conexión sendTimeAsDatetime.|
|setSendTimeAsDatetime void público (boolean sendTimeAsDateTimeValue)|Modifica la configuración de la propiedad de conexión sendTimeAsDatetime.|
     
  
 **Clase SQLServerDataSource**  
  
|Nombre|Description|  
|----------|-----------------|  
|setColumnEncryptionSetting void público (cadena columnEncryptionSetting)|Habilita o deshabilita la funcionalidad Always Encrypted para el objeto de origen de datos.<br /><br /> El valor predeterminado es Disabled.|  
|getColumnEncryptionSetting() de cadena pública|Recupera el valor de la funcionalidad Always Encrypted para el objeto de origen de datos.|
|setKeyStoreAuthentication void público (cadena keyStoreAuthentication)|Establece el nombre que identifica un almacén de claves. Solo el valor admitido es "JavaKeyStorePassword" para identifiying el almacén de claves de Java.<br/><br/>El valor predeterminado es null.|
|getKeyStoreAuthentication() de cadena pública|Obtiene el valor de la configuración de keyStoreAuthentication para el objeto de origen de datos.|
|setKeyStoreSecret void público (cadena keyStoreSecret)|Establece la contraseña para el almacén de claves de Java. Tenga en cuenta que, para el proveedor de almacén de claves de Java la contraseña para el almacén de claves y la clave debe ser el mismo. Tenga en cuenta que se debe establecer keyStoreAuthentication con "JavaKeyStorePassword".|
|setKeyStoreLocation void público (cadena keyStoreLocation)|Establece la ubicación incluido el nombre de archivo para el almacén de claves de Java. Tenga en cuenta que se debe establecer keyStoreAuthentication con "JavaKeyStorePassword".|
|getKeyStoreLocation() de cadena pública|Recupera el keyStoreLocation para el almacén de claves de Java.|
  
 **Clase SQLServerColumnEncryptionJavaKeyStoreProvider**  
  
 La implementación del proveedor de almacén de claves para el almacén de claves de Java. Esta clase permite usar certificados almacenados en el almacén de claves de Java como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionJavaKeyStoreProvider pública (cadena keyStoreLocation, char [] keyStoreSecret)|Proveedor de almacén de claves para el almacén de claves de Java.|  
  
 Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|pública byte [] decryptColumnEncryptionKey (masterKeyPath de cadena, cadena encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Descifra el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante el certificado con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso de clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadena, cadena, Byte[]).)|  
|pública byte [] encryptColumnEncryptionKey (masterKeyPath de cadena, cadena encryptionAlgorithm, byte [] plainTextColumnEncryptionKey)|Cifra una clave de cifrado de columna mediante el certificado con la ruta de acceso a la clave especificada y con el algoritmo especificado.<br /><br /> **El formato de la ruta de acceso de clave debe ser uno de los siguientes:**<br /><br /> Thumbprint:<huella_digital_certificado><br /><br /> Alias:<alias_certificado><br /><br /> (Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadena, cadena, Byte[]).)|  
|setName void público (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|pública getName de String)|Obtiene el nombre de este proveedor de almacén de claves.|
  
 **Clase SQLServerColumnEncryptionAzureKeyVaultProvider**  
  
 La implementación del proveedor de almacén de claves para el almacén de claves de Azure. Esta clase permite usar claves almacenadas en el almacén de claves de Azure como claves maestras de columna.  
  
 Constructores  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionAzureKeyVaultProvider pública (SQLServerKeyVaultAuthenticationCallback authenticationCallback, ExecutorService executorService)|Proveedor de almacén de claves para el almacén de claves de Azure.  Debe proporcionar una implementación para la interfaz SQLServerKeyVaultAuthenticationCallback recuperar un token de acceso para la clave en el almacén de claves de Azure.|  
  
 Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|pública byte [] decryptColumnEncryptionKey (masterKeyPath de cadena, cadena encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Descifra el valor cifrado especificado de una clave de cifrado de columna. Se espera el valor cifrado se cifre mediante la clave de la columna especificada IDmaster clave y mediante el algoritmo especificado. <br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. decryptColumnEncryptionKey (cadena, cadena, Byte[]).)|  
|pública byte [] encryptColumnEncryptionKey (masterKeyPath de cadena, cadena encryptionAlgorithm, byte [] columnEncryptionKey)|Cifra una clave de cifrado de columna con la clave maestra de columna especificada y utilizando el algoritmo especificado. <br />(Reemplaza a SQLServerColumnEncryptionKeyStoreProvider. encryptColumnEncryptionKey (cadena, cadena, Byte[]).)|  
|setName void público (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|pública getName de String)|Obtiene el nombre de este proveedor de almacén de claves.|  
  
  
 **Interfaz SQLServerKeyVaultAuthenticationCallback**  
  
 Esta interfaz contiene un método para la autenticación de almacén de claves de Azure, que consiste en ser implementada por el usuario.  
  
 Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|getAccessToken de cadena pública (entidad de cadena, recurso de cadena, cadena ámbito);|El método debe invalidarse. El método se utiliza para obtener acceso token al almacén de claves de Azure.|  
  
 **Clase SQLServerColumnEncryptionKeyStoreProvider**  
  
 Amplíe esta clase para implementar un proveedor del almacén de claves personalizado.  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Clase base para todos los proveedores del almacén de claves. Un proveedor personalizado debe derivar de esta clase y reemplazar sus funciones miembro y, a continuación, registrarla mediante SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Método de clase base para descifrar el valor cifrado especificado de una clave de cifrado de columna. Se espera que el valor cifrado se haya cifrado mediante la clave maestra de columna con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|Método de clase base para cifrar una clave de cifrado de columna mediante la clave maestra de columna con la ruta de acceso a la clave especificada y mediante el algoritmo especificado.|
|setName void abstracta público (nombre de cadena)|Establece el nombre de este proveedor de almacén de claves.|
|públicas abstractas getName() de cadena|Obtiene el nombre de este proveedor de almacén de claves.|  
  
 Métodos nuevo o que esté sobrecargados en **SQLServerPreparedStatement** (clase)  
  
|Nombre|Description|  
|----------|-----------------|  
|pública setBigDecimal void (int parameterIndex, BigDecimal x int precisión, escala de int)<br /><br /> public void setObject (int parameterIndex, objeto x, targetSqlType int, precisión de entero, escala de int)<br /><br /> public void setObject (int parameterIndex, objeto x, SQLType targetSqlType, precisión de entero, escala de entero)<br /><br /> public void setTime (parameterIndex int, java.sql.Time x, escala de int)<br /><br /> public void setTimestamp (parameterIndex int, java.sql.Timestamp, int escala x:) <br />public void setDateTimeOffset (int parameterIndex, microsoft.sql.DateTimeOffset x, escala de int)|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren precisión y la información de escala.|  
|pública setMoney void (int parameterIndex, BigDecimal x)<br /><br /> pública setSmallMoney void (int parameterIndex, BigDecimal x)<br /><br /> public void setUniqueIdentifier (int parameterIndex o guid de cadena)<br /><br /> setDateTime void público (parameterIndex int, java.sql.Timestamp x)<br /><br /> pública setSmallDateTime void (parameterIndex int, java.sql.Timestamp x)|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método setTimestamp() existente se usa para enviar los valores de parámetro a la columna cifrada datetime2. Cifrados de datetime y smalldatetime columnas utilice la nueva setDateTime() de métodos y setSmallDateTime() respectivamente.|  
|pública setBigDecimal void final (int parameterIndex, BigDecimal x int precisión, escala de int, boolean forceEncrypt)<br /><br /> pública setMoney void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> pública setSmallMoney void final (int parameterIndex, BigDecimal x forceEncrypt booleano)<br /><br /> setBoolean pública final void (parameterIndex int, boolean x, forceEncrypt booleano)<br /><br /> setByte pública final void (parameterIndex int, byte x forceEncrypt booleano)<br /><br /> setBytes pública final void (parameterIndex int, byte x[], forceEncrypt booleano)<br /><br /> pública setUniqueIdentifier void final (int parameterIndex, guid de cadena, booleano forceEncrypt)<br /><br /> setDouble pública final void (parameterIndex int, double x, forceEncrypt booleano)<br /><br /> setFloat pública final void (parameterIndex int, float x, forceEncrypt booleano)<br /><br /> pública setInt void final (parameterIndex int, el valor int, boolean forceEncrypt)<br /><br /> pública setLong void final (parameterIndex int, long x, forceEncrypt booleano)<br /><br /> pública final setObject (int parameterIndex, objeto x, targetSqlType int, precisión de entero, escala de int, boolean forceEncrypt)<br /><br /> pública setObject final void (int parameterIndex, objeto x, SQLType targetSqlType, precisión de entero, escala de entero, booleano forceEncrypt)<br /><br /> pública setShort void final (parameterIndex int, short x, forceEncrypt booleano)<br /><br /> setString void final pública (int parameterIndex, str de cadena, booleano forceEncrypt)<br /><br /> pública setNString void final (int parameterIndex, valor de cadena, booleano forceEncrypt)<br /><br /> pública setTime void final (parameterIndex int, java.sql.Time x, escala de int, boolean forceEncrypt)<br /><br /> pública setTimestamp void final (parameterIndex int, java.sql.Timestamp, int escala x, forceEncrypt booleano)<br /><br /> pública setDateTimeOffset void final (int parameterIndex, microsoft.sql.DateTimeOffset x, escala de int, boolean forceEncrypt)<br /><br /> setDateTime pública final void (parameterIndex int, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> pública setSmallDateTime void final (parameterIndex int, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> pública setDate void final (parameterIndex int, java.sql.Date x java.util.Calendar cal, forceEncrypt booleano)<br /><br /> pública setTime void final (parameterIndex int, java.sql.Time x java.util.Calendar cal, forceEncrypt booleano)<br /><br /> pública setTimestamp void final (parameterIndex int, java.sql.Timestamp x java.util.Calendar cal, forceEncrypt booleano)|Establece el parámetro designado en el valor de java determinado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no exigirá cifrado en los parámetros.|  
  
 Métodos nuevo o que esté sobrecargados en **SQLServerCallableStatement** (clase)  
  
|Nombre|Description|  
|----------|-----------------|  
|public void registerOutParameter (int parameterIndex, sqlType int, int precisión, escala de int)<br /><br /> public void registerOutParameter (int parameterIndex, SQLType sqlType, int precisión, escala de int)<br /><br /> public void registerOutParameter (cadena parameterName, sqlType int, int precisión, escala de int)<br /><br /> public void registerOutParameter (cadena parameterName, SQLType sqlType, int precisión, escala de int)<br />public void setBigDecimal (cadena parameterName, BigDecimal bd, int precisión, escala de int)<br /><br /> public void setTime (cadena parameterName, t java.sql.Time, escala de int)<br /><br /> public void setTimestamp (cadena parameterName, t java.sql.Timestamp, int escala)<br /><br /> public void setDateTimeOffset (cadena parameterName, microsoft.sql.DateTimeOffset t, int escala)<br/><br/>pública setObject final void (sCol de cadena, objeto x, targetSqlType int, precisión de entero, escala de int)|Estos métodos están sobrecargados con una precisión o un argumento de escala o ambos para admitir Always Encrypted para tipos de datos específicos que requieren precisión y la información de escala.|  
|setDateTime void público (cadena parameterName, java.sql.Timestamp x)<br /><br /> pública setSmallDateTime void (cadena parameterName, java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier (cadena parameterName o guid de cadena)<br /><br /> public void setMoney (cadena parameterName, BigDecimal bd)<br /><br /> public void setSmallMoney (cadena parameterName, BigDecimal bd)<br/><br/>getDateTime pública de marca de tiempo (int index)<br/><br/>getDateTime pública de marca de tiempo (cadena sCol)<br/><br/>pública getDateTime de marca de tiempo (índice de int, cal de calendario)<br/><br/>getSmallDateTime público de marca de tiempo (int index)<br/><br/>getSmallDateTime público de marca de tiempo (cadena sCol)<br/><br/>pública getSmallDateTime de marca de tiempo (índice de int, cal de calendario)<br/><br/>pública getSmallDateTime de marca de tiempo (nombre de la cadena, cal de calendario)<br/><br/>pública BigDecimal getMoney (int index)<br/><br/>pública BigDecimal getMoney (cadena sCol)<br/><br/>pública BigDecimal getSmallMoney (int index)<br/><br/>pública BigDecimal getSmallMoney (cadena sCol)|Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método setTimestamp() existente se usa para enviar los valores de parámetro a la columna cifrada datetime2. Cifrados de datetime y smalldatetime columnas utilice la nueva setDateTime() de métodos y setSmallDateTime() respectivamente.|  
|public void setObject (parameterName de cadena, o de objeto, int n, m int, forceEncrypt booleano)<br /><br /> public void setObject (parameterName de cadena, objeto obj, SQLType jdbcType, escala de int, forceEncrypt booleano)<br /><br /> setDate void público (cadena parameterName, java.sql.Date x c de calendario, forceEncrypt booleano)<br /><br /> public void setTime (cadena parameterName, java.sql.Time t, escala de int, boolean forceEncrypt)<br /><br /> setTime void público (cadena parameterName, java.sql.Time x c de calendario, forceEncrypt booleano)<br /><br /> public void setDateTime (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setDateTimeOffset (cadena parameterName, microsoft.sql.DateTimeOffset t, escala de int, boolean forceEncrypt)<br /><br /> public void setSmallDateTime (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setTimestamp (cadena parameterName, java.sql.Timestamp t, escala de int, boolean forceEncrypt)<br /><br /> public void setTimestamp (cadena parameterName, java.sql.Timestamp x forceEncrypt booleano)<br /><br /> public void setUniqueIdentifier (cadena parameterName, guid de cadena, booleano forceEncrypt)<br /><br /> public void setBytes (cadena parameterName, byte [] b, forceEncrypt booleano)<br /><br /> public void setByte (cadena parameterName, byte b, forceEncrypt booleano)<br /><br /> public void setString (cadena parameterName, s de cadena, booleano forceEncrypt)<br /><br /> pública setNString void final (parameterName de cadena, valor de cadena, booleano forceEncrypt)<br /><br /> public void setMoney (cadena parameterName, BigDecimal bd, forceEncrypt booleano)<br /><br /> public void setSmallMoney (cadena parameterName, BigDecimal bd, forceEncrypt booleano)<br /><br /> public void setBigDecimal (cadena parameterName, BigDecimal bd, int precisión, escala de int, forceEncrypt booleano)<br /><br /> public void setDouble (parameterName de cadena, doble d, forceEncrypt booleano)<br /><br /> public void setFloat (cadena parameterName, float f, forceEncrypt booleano)<br /><br /> pública setInt void (parameterName String, int i, forceEncrypt booleano)<br /><br /> public void setLong (cadena parameterName, long l, forceEncrypt booleano)<br /><br /> public void setShort (cadena parameterName, corta s, forceEncrypt booleano)<br /><br /> public void setBoolean (parameterNames de cadena, booleano b, forceEncrypt booleano)<br/><br/>pública setTimeStamp void (cadena sCol, java.sql.Timestamp x c de calendario, forceEncrypt booleano)|Establece el parámetro designado en el valor de java determinado.<br /><br /> Si el forceEncrypt booleano se establece en true, la consulta parámetro sólo se establecerá si la columna designación está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br /><br /> Si el forceEncrypt booleano se establece en false, el controlador no exigirá cifrado en los parámetros.|
 

 Métodos nuevo o que esté sobrecargados en **SQLServerResultSet** (clase)  
  
|Nombre|Description|  
|----------|-----------------|  
|getUniqueIdentifier de cadena pública (columnIndex int)<br/><br/>getUniqueIdentifier de cadena pública (cadena columnLabel)<br/><br/>   java.sql.Timestamp pública getDateTime (columnIndex int) <br/><br/> java.sql.Timestamp pública getDateTime (cadena nombredecolumna)   <br/><br/> java.sql.Timestamp pública getDateTime (int columnIndex, cal de calendario)   <br/><br/>java.sql.Timestamp pública getDateTime (cadena colName, cal de calendario)    <br/><br/>java.sql.Timestamp pública getSmallDateTime (columnIndex int)    <br/><br/> java.sql.Timestamp pública getSmallDateTime (cadena nombredecolumna)   <br/><br/> java.sql.Timestamp pública getSmallDateTime (int columnIndex, cal de calendario)   <br/><br/> java.sql.Timestamp pública getSmallDateTime (cadena colName, cal de calendario)   <br/><br/>  pública BigDecimal getMoney (columnIndex int)  <br/><br/> pública BigDecimal getMoney (cadena nombredecolumna)   <br/><br/> pública BigDecimal getSmallMoney (columnIndex int)   <br/><br/>  pública BigDecimal getSmallMoney (cadena nombredecolumna)  <br/><br/>pública updateMoney void (cadena columnName, BigDecimal x)    <br/><br/>  pública updateSmallMoney void (cadena columnName, BigDecimal x)  <br/><br/>     pública updateDateTime void (índice de int, java.sql.Timestamp x) <br/><br/> pública updateSmallDateTime void (índice de int, java.sql.Timestamp x) |Estos métodos se agregan para admitir Always Encrypted para los tipos de datos money, smallmoney, uniqueidentifier, datetime y smalldatetime. <br/><br/>Tenga en cuenta que el método updateTimestamp() existente se usa para actualizar las columnas datetime2 cifrados. Cifrados de datetime y smalldatetime columnas utilice la nueva updateDateTime() de métodos y updateSmallDateTime() respectivamente.|
|public void updateBoolean (índice de int, boolean x, forceEncrypt booleano)  <br/><br/>  public void updateByte (índice de int, byte x forceEncrypt booleano)  <br/><br/>  public void updateShort (índice int, short x, forceEncrypt booleano)  <br/><br/> public void updateInt (índice de int, int x forceEncrypt booleano)   <br/><br/>  public void updateLong (índice de int, long x, forceEncrypt booleano)  <br/><br/> public void updateFloat (índice de int, float x, forceEncrypt booleano)   <br/><br/> public void updateDouble (índice de int, double x, forceEncrypt booleano)   <br/><br/> updateMoney void público (índice de int, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateMoney void público (cadena columnName, BigDecimal x forceEncrypt booleano)  <br/><br/> updateSmallMoney void público (índice de int, BigDecimal x forceEncrypt booleano)   <br/><br/>  updateSmallMoney void público (cadena columnName, BigDecimal x forceEncrypt booleano)  <br/><br/> public void updateBigDecimal (int index, BigDecimal x precisión entero, escala de entero, booleano forceEncrypt)   <br/><br/>  public void updateString (int columnIndex, stringValue de cadena, booleano forceEncrypt)  <br/><br/>  public void updateNString (int columnIndex, nString de cadena, booleano forceEncrypt)  <br/><br/>  public void updateNString (cadena columnLabel, nString de cadena, booleano forceEncrypt)  <br/><br/> public void updateBytes (índice de int, byte x[], forceEncrypt booleano)   <br/><br/>  public void updateDate (índice de int, java.sql.Date x forceEncrypt booleano)  <br/><br/> pública updateTime void (índice de int, java.sql.Time x, escala de entero, booleano forceEncrypt)   <br/><br/> pública updateTimestamp void (índice de int, java.sql.Timestamp, int escala x, forceEncrypt booleano)   <br/><br/> pública updateDateTime void (índice de int, java.sql.Timestamp x, escala de entero, booleano forceEncrypt)   <br/><br/> pública updateSmallDateTime void (índice de int, java.sql.Timestamp x, escala de entero, booleano forceEncrypt)   <br/><br/>  pública updateDateTimeOffset void (índice de int, microsoft.sql.DateTimeOffset x, escala de entero, booleano forceEncrypt)  <br/><br/> updateUniqueIdentifier void público (índice de int, cadena x forceEncrypt booleano)    <br/><br/>  public void updateObject (int index, objeto x, int precisión, escala de int, boolean forceEncrypt)  <br/><br/>  público void updateObject (int índice, objeto obj, SQLType targetSqlType, escala de int, forceEncrypt booleano)  <br/><br/> public void updateBoolean (columnName de cadena, booleano x, forceEncrypt booleano)    <br/><br/>  public void updateByte (cadena columnName, bytes x forceEncrypt booleano)  <br/><br/>  public void updateShort (cadena columnName, x corto, forceEncrypt booleano)  <br/><br/> public void updateInt (columnName String, int x forceEncrypt booleano)   <br/><br/>   public void updateLong (cadena columnName, long x, forceEncrypt booleano) <br/><br/>  public void updateFloat (cadena columnName, float x, forceEncrypt booleano)  <br/><br/>  public void updateDouble (columnName de cadena, doble x, forceEncrypt booleano)  <br/><br/> updateBigDecimal void público (cadena columnName, BigDecimal x forceEncrypt booleano)   <br/><br/>  public void updateBigDecimal (cadena columnName, BigDecimal x precisión entero, escala de entero, booleano forceEncrypt)  <br/><br/> updateString void público (columnName de cadena, cadena x forceEncrypt booleano)   <br/><br/>  public void updateBytes (cadena columnName, x[] bytes, forceEncrypt booleano)  <br/><br/> public void updateDate (cadena columnName, java.sql.Date x forceEncrypt booleano)   <br/><br/>  pública updateTime void (cadena columnName, java.sql.Time x, escala de int, boolean forceEncrypt)  <br/><br/>  pública updateTimestamp void (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)  <br/><br/> pública updateDateTime void (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)   <br/><br/>  pública updateSmallDateTime void (cadena columnName, java.sql.Timestamp, int escala x, forceEncrypt booleano)  <br/><br/>  pública updateDateTimeOffset void (cadena columnName, microsoft.sql.DateTimeOffset x, escala de int, boolean forceEncrypt)  <br/><br/>  updateUniqueIdentifier void público (columnName de cadena, cadena x forceEncrypt booleano)<br/><br/>public void updateObject (columnName de cadena, objeto x, int precisión, escala de int, boolean forceEncrypt)<br/><br/>public void updateObject (columnName de cadena, objeto obj, SQLType targetSqlType, int escala, forceEncrypt booleano)|Actualice la columna designada con el valor de java especificado.<br/><br/>Si el forceEncrypt booleano se establece en true, la columna solo se establecerá si está cifrada y Always Encrypted está habilitado en la conexión o en la instrucción.<br/><br/>Si el forceEncrypt booleano se establece en false, el controlador no exigirá cifrado en los parámetros.|

  
Nuevos tipos en **microsoft.sql.Types** (clase)
|Nombre|Description|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Usar estos tipos como los tipos de SQL de destino al enviar valores de parámetro para **cifrados** datetime, smalldatetime, money, smallmoney, columnas uniqueidentifier con métodos setObject()/updateObject() API.|  
  
  
 **Enumeración SQLServerStatementColumnEncryptionSetting**  
  
 Especifica cómo se enviarán los datos y cómo se recibe al leer y escribir las columnas cifradas. Según su consulta específica, impacto en el rendimiento puede reducirse omitiendo el controlador de Always Encrypted procesamiento cuando se utilizan columnas sin cifrar. Tenga en cuenta que esta configuración no puede utilizarse para omitir el cifrado y obtener acceso a los datos de texto simple.  
  
 **Sintaxis**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Miembros**  
  
|Nombre|Description|  
|----------|-----------------|  
|UseConnectionSetting|Especifica que el comando de forma predeterminada la configuración siempre cifrado en la cadena de conexión.|  
|Habilitado|Habilita siempre cifrado para la consulta.|  
|ResultSetOnly|Especifica que solo los resultados del comando deben ser procesados por la rutina siempre cifrado en el controlador. Use este valor cuando el comando no tiene parámetros que requieren cifrado.|  
|Deshabilitado|Deshabilita siempre cifrado para la consulta.|  
  
 La configuración de nivel de instrucción para AE se agregan a la clase SQLServerConnection y a la clase SQLServerConnectionPoolProxy. Los siguientes métodos de estas clases están sobrecargados con la nueva configuración.  
  
|Nombre|Description|  
|----------|-----------------|  
|pública createStatement de instrucción (nLas int, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto de instrucción que genera objetos ResultSet con la configuración de cifrado de tipo, simultaneidad, capacidad de alojamiento y columna dada.|  
|pública prepareCall de CallableStatement (cadena sql, nLas int, nConcur int, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)|Crea un objeto CallableStatement con la configuración de cifrado de columna determinada que vaya a generar objetos ResultSet con el tipo dado, la simultaneidad y la capacidad de alojamiento.|  
|pública prepareStatement de PreparedStatement (cadena sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto de instrucción PreparedStatement con la opción de cifrado de columna especificada que tiene la capacidad de recuperar claves generadas automáticamente.|  
|pública prepareStatement de PreparedStatement (cadena sql, cadena [] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto de instrucción PreparedStatement con la configuración de cifrado de columna determinada que vaya a generar objetos ResultSet con los nombres de columna determinado.|  
|pública prepareStatement de PreparedStatement (cadena sql, int [] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|Crea un objeto de instrucción PreparedStatement con la configuración de cifrado de columna determinada que vaya a generar objetos ResultSet con los índices de columna determinada.|  
|pública prepareStatement de PreparedStatement (cadena sql, nLas int, nConcur int, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)|Crea un objeto de instrucción PreparedStatement con la configuración de cifrado de columna determinada que vaya a generar objetos ResultSet con el tipo dado, la simultaneidad y la capacidad de alojamiento.|  
  
> [!NOTE]  
>  Si Always Encrypted está deshabilitado para una consulta y la consulta tiene parámetros que deben estar cifrados (los parámetros que corresponden a las columnas cifradas), se producirá un error en la consulta.  
>   
>  Si Always Encrypted está deshabilitado para una consulta y la consulta devuelve los resultados de las columnas cifradas, la consulta devolverá valores cifrados. Los valores cifrados tendrá el tipo de datos varbinary.  
  
## <a name="see-also"></a>Vea también  
 [Usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  
  
