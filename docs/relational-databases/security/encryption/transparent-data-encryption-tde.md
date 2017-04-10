---
title: "Cifrado de datos transparente (TDE) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Cifrado de datos transparente"
  - "clave de cifrado de la base de datos, acerca de"
  - "TDE"
  - "clave de cifrado de la base de datos"
  - "TDE, acerca de"
  - "Cifrado de datos transparente (TDE), acerca de"
  - "cifrado [SQL Server], cifrado de datos transparente"
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
caps.latest.revision: 75
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 74
---
# Cifrado de datos transparente (TDE)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  El *Cifrado de datos transparente* (TDE) cifra los archivos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] y [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)], lo que se conoce como cifrado de datos en reposo. Puede tomar varias precauciones para proteger la base de datos, como diseñar un sistema seguro, cifrar los datos confidenciales e instalar un firewall alrededor de los servidores de bases de datos. Sin embargo, si se diera el caso de un robo de medios físicos (como unidades de disco o cintas de copia de seguridad), un usuario malintencionado solo tendría que restaurar o adjuntar la base de datos y examinar los datos. Una solución consiste en cifrar los datos confidenciales en la base de datos y usar un certificado para proteger las claves que se utilizan para cifrarlos. Esto evita que utilice los datos cualquiera que carezca de las claves, pero este tipo de protección debe planearse de antemano.  
  
 TDE realiza el cifrado y descifrado de E/S en tiempo real de los datos y los archivos de registro. El cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. La DEK es una clave simétrica protegida utilizando un certificado almacenado en la base de datos maestra del servidor o una clave asimétrica protegida por un módulo EKM. TDE protege los datos "en reposo", es decir, los archivos de datos y de registro. Ofrece la posibilidad de cumplir muchas leyes, normativas y directrices establecidas en diversos sectores. También permite a los desarrolladores de software cifrar los datos mediante algoritmos de cifrado AES y 3DES sin cambiar las aplicaciones existentes.  
  
> [!IMPORTANT]  
>  TDE no proporciona cifrado para los canales de comunicaciones. Para obtener más información sobre cómo cifrar datos en los canales de comunicación, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
>   
>  **Temas relacionados:**  
>   
>  -   [Cifrado de datos transparente con Base de datos SQL de Azure](../../../relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database.md)  
> -   [Introducción al cifrado de datos transparente (TDE) en SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
> -   [Mover una base de datos protegida por TDE a otra instancia de SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
> -   [Habilitar TDE en SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)   
> -   [Usar el conector de SQL Server con características de cifrado de SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [Blog de seguridad de SQL Server en TDE con las preguntas más frecuentes](https://blogs.msdn.microsoft.com/sqlsecurity/2016/10/05/feature-spotlight-transparent-data-encryption-tde/)
 
  
## <a name="about-tde"></a>Acerca de TDE  
 El cifrado del archivo de base de datos se realiza en el nivel de página. Las páginas de una base de datos cifrada se cifran antes de escribirse en el disco y se descifran cuando se leen en la memoria. TDE no aumenta el tamaño de la base de datos cifrada.  
  
 **Información aplicable a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**  
  
 Cuando se usa TDE con [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12, el certificado de nivel de servidor almacenado en la base de datos maestra lo crea [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] automáticamente. Para mover una base de datos TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], debe descifrar la base de datos, moverla y, luego, volver a habilitar TDE en el destino [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]. Para obtener instrucciones paso a paso para TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], consulte [Transparent Data Encryption with Azure SQL Database](../../../relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database.md).  
  
 **Información aplicable a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
 Una vez protegida, la base de datos puede restaurarse utilizando el certificado correcto. Para obtener más información acerca de los certificados, vea [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Al habilitar TDE, debería hacer inmediatamente una copia de seguridad del certificado y la clave privada asociada al certificado. Si el certificado no está disponible en algún momento o si debe restaurar o adjuntar la base de datos en otro servidor, debe tener copias de seguridad del certificado y la clave privada o no podrá abrir la base de datos. El cifrado del certificado se debería conservar aun cuando TDE deje de estar habilitado en la base de datos. Aunque la base de datos no se cifre, algunas partes del registro de transacciones pueden seguir estando protegidas y se puede necesitar el certificado para algunas operaciones hasta que se realice la copia de seguridad completa de la base de datos. Un certificado que ha excedido su fecha de expiración se puede seguir usando para cifrar y descifrar datos con TDE.  
  
 **Jerarquía de cifrado**  
  
 En la siguiente ilustración se muestra la arquitectura del cifrado TDE. Solo los elementos de nivel de base de datos (las partes de ALTER DATABASE y la clave de cifrado de base de datos son configurables por el usuario cuando se usa TDE en [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]).  
  
 ![Muestra la jerarquía descrita en el tema.](../../../relational-databases/security/encryption/media/tde-architecture.gif "Muestra la jerarquía descrita en el tema.")  
  
## <a name="using-transparent-data-encryption"></a>Utilizar el cifrado de datos transparente  
 Para usar TDE, siga estos pasos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
-   Cree una clave maestra  
  
-   Cree u obtenga un certificado protegido por la clave maestra  
  
-   Cree una clave de cifrado de base de datos y protéjala con el certificado  
  
-   Configure la base de datos para que utilice el cifrado  
  
 En el ejemplo siguiente se muestra cómo cifrar y descifrar la base de datos `AdventureWorks2012` mediante un certificado instalado en el servidor denominado `MyServerCert`.  
  
```  
USE master;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
go  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
go  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION ON;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]programa las operaciones de cifrado y descifrado en subprocesos que se ejecutan en segundo plano. Puede ver el estado de estas operaciones mediante las vistas de catálogo y las vistas de administración dinámica de la lista que se muestra más adelante en este tema.  
  
> [!CAUTION]  
>  Los archivos de copia de seguridad de las bases de datos que tienen habilitado TDE también se cifran mediante la clave de cifrado de la base de datos. Como consecuencia, al restaurar estas copias de seguridad debe estar disponible el certificado que protege la clave de cifrado de la base de datos. Esto significa que, además de hacer copias de seguridad de la base de datos, tiene que asegurarse de que mantiene copias de seguridad de los certificados del servidor para evitar la pérdida de datos. Si el certificado deja de estar disponible, perderá los datos. Para obtener más información, consulte [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
## <a name="commands-and-functions"></a>Comandos y funciones  
 Para que puedan ser aceptados por las instrucciones siguientes, los certificados de TDE deben cifrarse con la clave maestra de la base de datos. Si solamente se cifran con una contraseña, las instrucciones los rechazarán como sistemas de cifrado.  
  
> [!IMPORTANT]  
>  Si los certificados se protegen mediante contraseña una vez usados para TDE, la base de datos dejará de ser accesible después de un reinicio.  
  
 En la tabla siguiente se proporcionan vínculos y explicaciones de los comandos y funciones de TDE.  
  
|Comando o función|Finalidad|  
|-------------------------|-------------|  
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|Crea una clave que se utiliza para cifrar una base de datos.|  
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Cambia la clave que se utiliza para cifrar una base de datos.|  
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Quita la clave que se utilizó para cifrar una base de datos.|  
|[Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)|Explica la opción **ALTER DATABASE** que se utiliza para habilitar TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Vistas de catálogo y vistas de administración dinámica  
 En la tabla siguiente se muestran las vistas de catálogo y las vistas de administración dinámica de TDE.  
  
|Vista de catálogo o vista de administración dinámica|Finalidad|  
|---------------------------------------------|-------------|  
|[sys.databases &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista de catálogo que muestra información sobre las bases de datos.|  
|[sys.certificates &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista de catálogo que muestra los certificados de una base de datos.|  
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|Vista de administración dinámica que proporciona información sobre las claves de cifrado utilizadas en una base de datos y el estado de cifrado de una base de datos.|  
  
## <a name="permissions"></a>Permisos  
 Cada una de las características y comandos de TDE tiene sus propios requisitos de permisos, que se describen en las tablas mostradas anteriormente.  
  
 Para ver los metadatos relacionados con TDE, se requiere el permiso VIEW DEFINITION en el certificado.  
  
## <a name="considerations"></a>Consideraciones  
 Mientras se realiza el examen del proceso de nuevo cifrado para una operación de cifrado de base de datos, las operaciones de mantenimiento de la base de datos están deshabilitadas. Puede configurar la base de datos en modo de usuario único si desea realizar la operación de mantenimiento. Para obtener más información, vea [Establecer una base de datos en modo de usuario único](../../../relational-databases/databases/set-a-database-to-single-user-mode.md).  
  
 Puede encontrar el estado del cifrado de la base de datos utilizando la vista de administración dinámica sys.dm_database_encryption_keys. Para obtener más información, vea la sección "Vistas de catálogo y vistas de administración dinámica", anteriormente en este tema.  
  
 En TDE, se cifran todos los archivos y grupos de archivos de la base de datos. Si algún grupo de archivos de una base de datos está marcado como READ ONLY, se producirá un error en la operación de cifrado de la base de datos.  
  
 Si una base de datos se utiliza en una creación de reflejo de la base de datos o en un trasvase de registros, se cifrarán ambas bases de datos. Las transacciones del registro se cifrarán cuando se envíen entre ellas.  
  
> [!IMPORTANT]  
>  Los índices de texto completo se cifrarán cuando una base de datos esté configurada para cifrarse. Los índices de texto completo creados antes de SQL Server 2008 se importarán a la base de datos durante la actualización a SQL Server 2008 o posterior y se cifrarán mediante TDE.  
  
  
### <a name="restrictions"></a>Restricciones  
 No están permitidas las operaciones siguientes durante el cifrado inicial de la base de datos, el cambio clave o el descifrado de una base de datos:  
  
-   Quitar un archivo de un grupo de archivos de la base de datos.  
  
-   Quitar la base de datos.  
  
-   Dejar sin conexión la base de datos.  
  
-   Separar la base de datos.  
  
-   Pasar la base de datos o el grupo de archivos al estado READ ONLY.  
  
 No están permitidas las operaciones siguientes durante la ejecución de instrucciones CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY o ALTER DATABASE...SET ENCRYPTION.  
  
-   Quitar un archivo de un grupo de archivos de la base de datos.  
  
-   Eliminar la base de datos.  
  
-   Dejar sin conexión la base de datos.  
  
-   Separar la base de datos.  
  
-   Pasar la base de datos o el grupo de archivos al estado READ ONLY.  
  
-   Usar un comando ALTER DATABASE.  
  
-   Iniciar una copia de seguridad de base de datos o de archivos de base de datos.  
  
-   Iniciar una restauración de base de datos o de archivos de base de datos.  
  
-   Crear una instantánea.  
  
 Las operaciones o condiciones siguientes impedirán la ejecución de las instrucciones CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY o ALTER DATABASE...SET ENCRYPTION.  
  
-   La base de datos o cualquiera de sus grupos de archivos son de solo lectura.  
  
-   Se está ejecutando un comando ALTER DATABASE.  
  
-   Se está ejecutando cualquier tipo de copia de seguridad de los datos.  
  
-   La base de datos está sin conexión o en restauración.  
  
-   Se está realizando una instantánea.  
  
-   Se están realizando tareas de mantenimiento en la base de datos.  
  
 Al crear los archivos de base de datos, la inicialización instantánea de archivos no está disponible cuando TDE está habilitado.  
  
 Para cifrar la clave de cifrado de la base de datos con una clave asimétrica, la clave asimétrica debe residir en un proveedor extensible de administración de claves.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>El cifrado de datos transparente y los registros de transacciones  
 Al habilitar una base de datos para utilizar TDE, se "pone a cero" la parte restante del registro de transacciones virtual para exigir el registro de transacciones virtual siguiente. Esto garantiza que no quede ningún texto sin cifrar en los registros de transacciones una vez configurada la base de datos para el cifrado. Puede encontrar el estado del cifrado del archivo de registro en la columna `encryption_state` de la vista `sys.dm_database_encryption_keys`, como en este ejemplo:  
  
```  
USE AdventureWorks2012;  
GO  
/* The value 3 represents an encrypted state   
   on the database and transaction logs. */  
SELECT *  
FROM sys.dm_database_encryption_keys  
WHERE encryption_state = 3;  
GO  
```  
  
 Para obtener más información sobre la arquitectura de los archivos de registro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [El registro de transacciones &#40;SQL Server&#41;](../../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Todos los datos escritos en el registro de transacciones antes de cambiar la clave de cifrado de la base de datos se cifrarán mediante la clave de cifrado anterior de la base de datos.  
  
 Cuando una clave de cifrado de base de datos se modifica dos veces, debe realizarse una copia de seguridad de registros para que la clave de cifrado de base de datos pueda volver a modificarse.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>El cifrado de datos transparente y la base de datos del sistema tempdb  
 La base de datos del sistema tempdb se cifrará si alguna otra base de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se cifra mediante TDE. Esto podría tener un efecto en el rendimiento de las bases de datos no cifradas de la misma instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información sobre la base de datos del sistema tempdb, vea [Bade de datos tempdb](../../../relational-databases/databases/tempdb-database.md).  
  
### <a name="transparent-data-encryption-and-replication"></a>Cifrado de datos transparente y replicación  
 La replicación no replica automáticamente los datos de una base de datos habilitada para TDE en un formato cifrado. Debe habilitar por separado TDE si desea proteger las bases de datos de suscriptor y de distribución. La replicación de instantáneas, así como la distribución inicial de datos para la replicación transaccional y de mezcla, puede almacenar los datos en archivos intermedios sin cifrar; por ejemplo, los archivos bcp.  Durante la replicación transaccional o de mezcla, el cifrado puede habilitarse para proteger el canal de comunicaciones. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
### <a name="transparent-data-encryption-and-filestream-data"></a>Cifrado de datos transparente y FILESTREAM DATA  
 Los datos FILESTREAM no se cifran ni siquiera cuando se habilita TDE.  
  
## <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Cifrado de datos transparente y extensión del grupo de búferes  
 Los archivos relacionados con la extensión del grupo de búferes (BPE) no se cifran si la base de datos se cifra con TDE. Debe usar herramientas de cifrado de nivel de sistema de archivos, como Bitlocker o EFS, para archivos relacionados con BPE.  
  
## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Cifrado de datos transparente y OLTP en memoria  
 El TDE se puede habilitar en una base de datos que tenga objetos de OLTP en memoria. En [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], los datos y registros de OLTP en memoria se cifran si TDE está habilitado. En [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], los registros de OLTP en memoria se cifran si TDE está habilitado, pero los archivos del grupo de archivos MEMORY_OPTIMIZED_DATA no se cifran.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Mover una base de datos protegida por TDE a otra instancia de SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
 [Habilitar TDE en SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
 [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Cifrado de datos transparente con Base de datos SQL de Azure](../../../relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database.md)  
 [Introducción al cifrado de datos transparente (TDE) en SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
 [Cifrado de SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)  
 [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
   
## <a name="see-also"></a>Vea también  
 [Centro de seguridad para el motor de base de datos SQL Server y la base de datos SQL Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)  
  
  