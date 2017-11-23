---
title: sp_addlinkedserver (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs: TSQL
helpviewer_keywords: sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
caps.latest.revision: "70"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 35173890392c69d6ef6fe40c71b484ae9db3bee3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddlinkedserver-transact-sql"></a>sp_addlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un servidor vinculado. Un servidor vinculado permite obtener acceso a consultas heterogéneas distribuidas en orígenes de datos OLE DB. Después de crea un servidor vinculado mediante el uso de **sp_addlinkedserver**distribuidas se pueden ejecutar consultas en este servidor. Si el servidor vinculado se define como una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden ejecutar procedimientos almacenados remotos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server=** ] **'***server***'**  
 Es el nombre del servidor vinculado que se va a crear. *server* es de tipo **sysname**y no tiene ningún valor predeterminado.  
  
 [  **@srvproduct=** ] **'***product_name***'**  
 Es el nombre del producto del origen de datos OLE DB para agregarlo como servidor vinculado. *product_name* es **nvarchar (**128**)**, su valor predeterminado es null. Si **SQL Server**, *NombreProveedor*, *data_source*, *ubicación*, *provider_string*, y *catálogo* no tienen que especificarse.  
  
 [  **@provider=** ] **'***NombreProveedor***'**  
 Es el identificador de programación (PROGID) único del proveedor OLE DB que corresponde a este origen de datos. *NombreProveedor* debe ser único para el proveedor OLE DB especificado instalado en el equipo actual. *NombreProveedor* es **nvarchar (**128**)**, su valor predeterminado es NULL; sin embargo, si *NombreProveedor* es se omite, se utilizará SQLNCLI. (El uso de SQLNCLI y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redirigirá a la última versión del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client). Se espera que el proveedor OLE DB se registre con el PROGID especificado en el registro.  
  
 [  **@datasrc=** ] **'***data_source***'**  
 Es el nombre del origen de datos como lo interpreta el proveedor OLE DB. *data_source* es **nvarchar (**4000**)**. *data_source* se pasa como la propiedad DBPROP_INIT_DATASOURCE para inicializar el proveedor OLE DB.  
  
 [  **@location=** ] **'***ubicación***'**  
 Es la ubicación de la base de datos según la interpretación del proveedor OLE DB. *ubicación* es **nvarchar (**4000**)**, su valor predeterminado es null. *ubicación* se pasa como la propiedad DBPROP_INIT_LOCATION para inicializar el proveedor OLE DB.  
  
 [  **@provstr=** ] **'***provider_string***'**  
 Es la cadena de conexión específica del proveedor OLE DB que identifica un origen de datos único. *provider_string* es **nvarchar (**4000**)**, su valor predeterminado es null. *provstr* se pasa a IDataInitialize o se establece como la propiedad DBPROP_INIT_PROVIDERSTRING para inicializar el proveedor OLE DB.  
  
 Cuando se crea el servidor vinculado para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, la instancia puede especificarse mediante la palabra clave SERVER como servidor =*servername*\\*nombreDeInstancia*para especificar una instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *ServerName* es el nombre del equipo en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando, y *nombreDeInstancia* es el nombre de la instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que se conectará el usuario.  
  
> [!NOTE]  
>  Para tener acceso a una base de datos reflejada, una cadena de conexión debe contener el nombre de la base de datos. Este nombre es necesario para que el proveedor de acceso a datos pueda intentar la conmutación por error. La base de datos se puede especificar en el  **@provstr**  o  **@catalog**  parámetro. Opcionalmente, la cadena de conexión también puede proporcionar un nombre de asociado de conmutación por error.  
  
 [  **@catalog=** ] **'***catálogo***'**  
 Es el catálogo que se utilizará cuando se realiza una conexión al proveedor OLE DB. *catálogo* es **sysname**, su valor predeterminado es null. *catálogo* se pasa como la propiedad DBPROP_INIT_CATALOG para inicializar el proveedor OLE DB. Cuando se define el servidor vinculado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], catalog se refiere a la base de datos predeterminada a la que se asigna el servidor vinculado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se muestran las distintas maneras de configurar un servidor vinculado para los orígenes de datos a los que se puede tener acceso a través de OLE DB. Existen varias formas de configurar un servidor vinculado para un origen de datos determinado; puede haber más de una fila por tipo de origen de datos. Esta tabla también muestra el **sp_addlinkedserver** valores de parámetro que se usará para configurar el servidor vinculado.  
  
|Origen de datos remotos de OLE DB|Proveedor OLE DB|product_name|provider_name|data_source|ubicación|provider_string|catálogo|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proveedor native Client OLE DB|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<sup>1</sup> (valor predeterminado)||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proveedor native Client OLE DB||**SQLNCLI**|Nombre de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (para la instancia predeterminada)|||Nombre de la base de datos (opcional)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proveedor native Client OLE DB||**SQLNCLI**|*ServerName*\\*nombreDeInstancia* (para la instancia específica)|||Nombre de la base de datos (opcional)|  
|Oracle, versión 8 y posterior|Proveedor Oracle para OLE DB|Cualquiera|**OraOLEDB.Oracle**|Alias para base de datos Oracle||||  
|Access/Jet|Proveedor Microsoft OLE DB para Jet|Cualquiera|**Microsoft.Jet.OLEDB.4.0**|Ruta de acceso completa del archivo de base de datos Jet||||  
|Origen de datos ODBC|Proveedor Microsoft OLE DB para ODBC|Cualquiera|**MSDASQL**|DSN del sistema del origen de datos ODBC||||  
|Origen de datos ODBC|Proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para ODBC|Cualquiera|**MSDASQL**|||Cadena de conexión ODBC||  
|Sistema de archivos|Proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Servicios de Index Server|Cualquiera|**MSIDXS**|Nombre de catálogo de Servicios de Index Server||||  
|Hojas de cálculo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel|Proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet|Cualquiera|**Microsoft.Jet.OLEDB.4.0**|Ruta de acceso completa del archivo Excel||Excel 5.0||  
|Base de datos IBM DB2|Proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para DB2|Cualquiera|**DB2OLEDB**|||Vea [!INCLUDE[msCoName](../../includes/msconame-md.md)] proveedor OLE DB para DB2 documentación.|Nombre del catálogo de la base de datos DB2|  
  
 <sup>1</sup> esta forma de configurar un servidor vinculado obliga el nombre del servidor vinculado sea igual que el nombre de red de la instancia remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use *data_source* para especificar el servidor.  
  
 <sup>2</sup> "Cualquiera" indica que el nombre del producto puede ser cualquier cosa.  
  
 El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB es el proveedor que se usa con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si no se especifica ningún nombre de proveedor o si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se especifica como el nombre del producto. Incluso si especifica el nombre de proveedor antiguo, SQLOLEDB, éste se cambiará a SQLNCLI cuando se mantenga en el catálogo.  
  
 El *data_source*, *ubicación*, *provider_string*, y *catálogo* parámetros identifican la base de datos o bases de datos de la que está vinculadas que apunta el servidor. Si alguno de estos parámetros es NULL, no se establecerá la propiedad de inicialización de OLE DB correspondiente.  
  
 En un entorno en clúster, al especificar nombres de archivo para apuntar a orígenes de datos OLE DB, utilice el nombre UNC (convención de nomenclatura universal) o una unidad compartida para especificar la ubicación.  
  
 **sp_addlinkedserver** no puede ejecutarse en una transacción definida por el usuario.  
  
> [!IMPORTANT]  
>  Cuando se crea un servidor vinculado mediante **sp_addlinkedserver**, se agrega una autoasignación del valor predeterminado para todos los inicios de sesión locales. En el caso de proveedores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los inicios de sesión autenticados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden obtener acceso al proveedor con la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los administradores deben tener en cuenta el uso de `sp_droplinkedsrvlogin <linkedserver_name>, NULL` para quitar la asignación global.  
  
## <a name="permissions"></a>Permissions  
 El `sp_addlinkedserver` instrucción requiere el `ALTER ANY LINKED SERVER` permiso. (SSMS **nuevo servidor vinculado** cuadro de diálogo se implementa de modo que debe pertenecer el `sysadmin` rol fijo de servidor.)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-microsoft-sql-server-native-client-ole-db-provider"></a>A. Usar el proveedor OLE DB de Microsoft SQL Server Native Client  
 En el siguiente ejemplo se crea un servidor vinculado denominado `SEATTLESales`. El nombre del producto es `SQL Server` y no se utiliza ningún nombre de proveedor.  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  
  
 En el ejemplo siguiente se crea un servidor vinculado `S1_instance1` en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.  
  
```  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>B. Usar el proveedor Microsoft OLE DB para Microsoft Access  
 El proveedor de Microsoft.Jet.OLEDB.4.0 conecta a las bases de datos de Microsoft Access que usan el formato 2002-2003. En el siguiente ejemplo se crea un servidor vinculado denominado `SEATTLE Mktg`.  
  
> [!NOTE]  
>  En este ejemplo se da por supuesto que ambos [!INCLUDE[msCoName](../../includes/msconame-md.md)] acceso y el ejemplo **Northwind** base de datos están instalados y que la **Northwind** base de datos reside en C:\Msoffice\Access\Samples.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 El proveedor de Microsoft.ACE.OLEDB.12.0 conecta a las bases de datos de Microsoft Access que usan el formato 2007. En el siguiente ejemplo se crea un servidor vinculado denominado `SEATTLE Mktg`.  
  
> [!NOTE]  
>  En este ejemplo se da por supuesto que ambos [!INCLUDE[msCoName](../../includes/msconame-md.md)] acceso y el ejemplo **Northwind** base de datos están instalados y que la **Northwind** base de datos reside en C:\Msoffice\Access\Samples.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-datasource-parameter"></a>C. Usar el proveedor Microsoft OLE DB para ODBC con el parámetro data_source  
 En el ejemplo siguiente se crea un servidor vinculado denominado `SEATTLE Payroll` que usa el [!INCLUDE[msCoName](../../includes/msconame-md.md)] proveedor OLE DB para ODBC (`MSDASQL`) y la *data_source* parámetro.  
  
> [!NOTE]  
>  El nombre del origen de datos ODBC especificado debe definirse como DSN del sistema en el servidor antes de utilizar el servidor vinculado.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. Usar el proveedor Microsoft OLE DB para una hoja de cálculo de Excel  
 Para crear una definición de servidor vinculado mediante el [!INCLUDE[msCoName](../../includes/msconame-md.md)] proveedor OLE DB para Jet tener acceso a una hoja de cálculo de Excel en el formato 1997-2003, cree primero un rango con nombre en Excel mediante la especificación de las columnas y filas de la hoja de cálculo de Excel para seleccionar. Entonces, podrá hacerse referencia al nombre del intervalo como un nombre de tabla en una consulta distribuida.  
  
```  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 Para obtener acceso a los datos de una hoja de cálculo Excel, asocie un nombre a un intervalo de celdas. La consulta siguiente se puede utilizar para obtener acceso al intervalo denominado `SalesData` especificado como una tabla utilizando el servidor vinculado que se creó anteriormente.  
  
```  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en una cuenta de dominio que tiene acceso a un recurso compartido remoto, se puede utilizar una ruta de acceso UNC en lugar de una unidad asignada.  
  
```  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 Para conectarse a una hoja de cálculo de Excel en formato de Excel 2007, use el proveedor ACE.  
  
```  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. Usar el proveedor Microsoft OLE DB para Jet para tener acceso a un archivo de texto  
 En este ejemplo se crea un servidor vinculado para obtener acceso directamente a archivos de texto, sin necesidad de vincular los archivos como tablas en un archivo .mdb de Access. El proveedor es `Microsoft.Jet.OLEDB.4.0` y la cadena de proveedor es `Text`.  
  
 El origen de datos es la ruta de acceso completa del directorio que contiene los archivos de texto. En el mismo directorio que los archivos de texto, debe existir un archivo schema.ini, que describe la estructura de dichos archivos. Para obtener más información sobre cómo crear un archivo schema.ini, vea la documentación relativa al motor de bases de datos Jet.  
  
```  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. Usar el proveedor Microsoft OLE DB para DB2  
 En el siguiente ejemplo se crea un servidor vinculado llamado `DB2` que utiliza el `Microsoft OLE DB Provider for DB2`.  
  
```  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-includesssdsfullincludessssdsfull-mdmd-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premise-databases"></a>G. Agregar una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como un servidor vinculado para su uso con consultas distribuidas en bases de datos en la nube y locales  
 Puede agregar una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como un servidor vinculado y después utilizarlo con consultas distribuidas que abarcan las bases de datos locales y en la nube. Se trata de un componente para soluciones híbridas de base de datos que abarcan varias redes corporativas locales y la nube de Windows Azure.  
  
 El producto del cuadro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene la característica de consulta distribuida, que permite escribir consultas para combinar datos de orígenes de datos locales y datos de orígenes remotos (incluidos datos de orígenes de datos que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) definidos como servidores vinculados. Cada [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (excepto la base de datos maestra virtual) se puede agregar como un servidor vinculado individual y utilizar después directamente en las aplicaciones de base de datos como cualquier otra base de datos.  
  
 Entre las ventajas de utilizar [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] se incluyen facilidad de uso, alta disponibilidad, escalabilidad, trabajo con un modelo de desarrollo conocido y un modelo de datos relacional. Los requisitos de la aplicación de base de datos determinan cómo utilizar [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] en la nube. Puede mover todos los datos a la vez a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] o mover progresivamente algunos de los datos y conservar los datos restantes de forma local. Para una aplicación de base de datos híbrida como esta, ahora se puede agregar [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como servidores vinculados y la aplicación de base de datos puede emitir consultas distribuidas para combinar datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] y orígenes de datos locales.  
  
 A continuación se muestra un ejemplo simple que explica cómo conectarse a una [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] mediante consultas distribuidas:  
  
```  
------ Configure the linked server  
-- Add one Windows Azure SQL DB as Linked Server  
EXEC sp_addlinkedserver  
@server='myLinkedServer', -- here you can specify the name of the linked server  
@srvproduct='',       
@provider='sqlncli', -- using SQL Server Native Client  
@datasrc='myServer.database.windows.net',   -- add here your server name  
@location='',  
@provstr='',  
@catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  
-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
@rmtsrvname = 'myLinkedServer',  
@useself = 'false',  
@rmtuser = 'myLogin',             -- add here your login on Azure DB  
@rmtpassword = 'myPassword' -- add here your password on Azure DB  
EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  
------ Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
exec ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
exec ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
select * from myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>Vea también  
 [Las consultas distribuidas almacenan procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [sp_setnetname &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
