---
title: Cifrado de datos transparente
description: El cifrado de datos transparente (TDE) para almacenamiento de datos paralelos (PDW) realiza el cifrado y descifrado de e/s en tiempo real de los archivos de datos y de registro de transacciones, así como los archivos de registro de PDW especiales.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e75230ed175c6fbf1b0a2492265bbe12067060ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399932"
---
# <a name="transparent-data-encryption"></a>Cifrado de datos transparente
Puede tomar varias precauciones para ayudar a proteger la base de datos, como diseñar un sistema seguro, cifrar los recursos confidenciales e instalar un firewall alrededor de los servidores de base de datos. Sin embargo, para un escenario en el que se roban los medios físicos (como unidades o cintas de copia de seguridad), un usuario malintencionado solo puede restaurar o adjuntar la base de datos y examinar los datos. Una solución consiste en cifrar los datos confidenciales en la base de datos y usar un certificado para proteger las claves que se utilizan para cifrarlos. Esto evita que utilice los datos cualquiera que carezca de las claves, pero este tipo de protección debe planearse de antemano.  
  
El *cifrado de datos transparente* (TDE) realiza el cifrado y descifrado de e/s en tiempo real de los archivos de registro de transacciones y de datos y los archivos de registro de PDW especiales. El cifrado usa una clave de cifrado de base de datos (DEK), que se almacena en el registro de arranque de la base de datos de disponibilidad durante la recuperación. DEK es una clave simétrica protegida mediante un certificado almacenado en la base de datos maestra del PDW de SQL Server. TDE protege los datos "en reposo", es decir, los archivos de datos y de registro. Ofrece la posibilidad de cumplir muchas leyes, normativas y directrices establecidas en diversos sectores. Esta característica permite a los desarrolladores de software cifrar los datos mediante algoritmos de cifrado AES y 3DES sin cambiar las aplicaciones existentes.  
  
> [!IMPORTANT]  
> TDE no proporciona cifrado para los datos que viajan entre el cliente y el PDW. Para obtener más información sobre cómo cifrar los datos entre el cliente y PDW de SQL Server, consulte [aprovisionamiento de un certificado](provision-certificate.md).  
>   
> TDE no cifra los datos mientras se mueven o se usan. No se cifra el tráfico interno entre los componentes de PDW dentro del PDW de SQL Server. Los datos almacenados temporalmente en búferes de memoria no están cifrados. Para mitigar este riesgo, controle el acceso físico y las conexiones a la PDW de SQL Server.  
  
Una vez protegida, la base de datos puede restaurarse utilizando el certificado correcto.  
  
> [!NOTE]  
> Cuando cree un certificado para TDE, debe hacer una copia de seguridad inmediatamente, junto con la clave privada asociada. Si el certificado no está disponible en algún momento o si debe restaurar o adjuntar la base de datos en otro servidor, debe tener copias de seguridad del certificado y la clave privada o no podrá abrir la base de datos. El cifrado del certificado se debería conservar aun cuando TDE deje de estar habilitado en la base de datos. Aunque la base de datos no se cifre, algunas partes del registro de transacciones pueden seguir estando protegidas y se puede necesitar el certificado para algunas operaciones hasta que se realice la copia de seguridad completa de la base de datos. Un certificado que ha excedido su fecha de expiración se puede seguir usando para cifrar y descifrar datos con TDE.  
  
El cifrado del archivo de base de datos se realiza en el nivel de página. Las páginas de una base de datos cifrada se cifran antes de escribirse en el disco y se descifran cuando se leen en la memoria. TDE no aumenta el tamaño de la base de datos cifrada.  
  
En la siguiente ilustración se muestra la jerarquía de claves para el cifrado de TDE:  
  
![Muestra la jerarquía](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Utilizar el cifrado de datos transparente  
Para usar TDE, siga estos pasos. Los tres primeros pasos solo se realizan una vez, al preparar PDW de SQL Server para admitir TDE.  
  
1.  Cree una clave maestra en la base de datos maestra.  
  
2.  Use **sp_pdw_database_encryption** para habilitar TDE en el PDW de SQL Server. Esta operación modifica las bases de datos temporales con el fin de garantizar la protección de los datos temporales futuros y producirá un error si se intenta cuando haya sesiones activas con tablas temporales. **sp_pdw_database_encryption** activa el enmascaramiento de datos del usuario en los registros del sistema de PDW. (Para obtener más información acerca del enmascaramiento de datos de usuario en los registros del sistema de PDW, vea [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)).  
  
3.  Utilice [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) para crear una credencial que pueda autenticarse y escribir en el recurso compartido donde se almacenará la copia de seguridad del certificado. Si ya existe una credencial para el servidor de almacenamiento deseado, puede usar la credencial existente.  
  
4.  En la base de datos maestra, cree un certificado protegido por la clave maestra.  
  
5.  Realice una copia de seguridad del certificado en el recurso compartido de almacenamiento.  
  
6.  En la base de datos de usuario, cree una clave de cifrado de base de datos y protéjala con el certificado almacenado en la base de datos maestra.  
  
7.  Use la `ALTER DATABASE` instrucción para cifrar la base de datos mediante TDE.  
  
En el ejemplo siguiente se muestra cómo cifrar la `AdventureWorksPDW2012` base de datos `MyServerCert`mediante un certificado denominado, creado en PDW de SQL Server.  
  
**Primero: habilite TDE en el PDW de SQL Server.** Esta acción solo es necesaria una vez.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**Segundo: crear y hacer una copia de seguridad de un certificado en la base de datos maestra.** Esta acción solo es necesaria una vez. Puede tener un certificado independiente para cada base de datos (recomendado) o puede proteger varias bases de datos con un certificado.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**Last: cree DEK y use ALTER DATABASE para cifrar una base de datos de usuario.** Esta acción se repite para cada base de datos protegida por TDE.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
Las operaciones de cifrado y descifrado se programan en subprocesos en segundo plano mediante SQL Server. Puede ver el estado de estas operaciones mediante las vistas de catálogo y las vistas de administración dinámica de la lista que aparece más adelante en este artículo.  
  
> [!CAUTION]  
> Los archivos de copia de seguridad de las bases de datos que tienen habilitado TDE también se cifran mediante la clave de cifrado de la base de datos. Como consecuencia, al restaurar estas copias de seguridad debe estar disponible el certificado que protege la clave de cifrado de la base de datos. Esto significa que, además de hacer copias de seguridad de la base de datos, tiene que asegurarse de que mantiene copias de seguridad de los certificados del servidor para evitar la pérdida de datos. Si el certificado deja de estar disponible, perderá los datos.  
  
## <a name="commands-and-functions"></a>Comandos y funciones  
Para que puedan ser aceptados por las instrucciones siguientes, los certificados de TDE deben cifrarse con la clave maestra de la base de datos.  
  
En la tabla siguiente se proporcionan vínculos y explicaciones de los comandos y funciones de TDE.  
  
|Comando o función|Propósito|  
|-----------------------|-----------|  
|[CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Crea una clave que se utiliza para cifrar una base de datos.|  
|[MODIFICAR LA CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Cambia la clave que se utiliza para cifrar una base de datos.|  
|[QUITAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Quita la clave que se utilizó para cifrar una base de datos.|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Explica la opción **ALTER DATABASE** que se utiliza para habilitar TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Vistas de catálogo y vistas de administración dinámica  
En la tabla siguiente se muestran las vistas de catálogo y las vistas de administración dinámica de TDE.  
  
|Vista de catálogo o vista de administración dinámica|Propósito|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista de catálogo que muestra información sobre las bases de datos.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista de catálogo que muestra los certificados de una base de datos.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Vista de administración dinámica que proporciona información para cada nodo, sobre las claves de cifrado utilizadas en una base de datos y el estado de cifrado de una base de datos.|  
  
## <a name="permissions"></a>Permisos  
Cada una de las características y comandos de TDE tiene sus propios requisitos de permisos, que se describen en las tablas mostradas anteriormente.  
  
La visualización de los metadatos relacionados con `CONTROL SERVER` TDE requiere el permiso.  
  
## <a name="considerations"></a>Consideraciones  
Mientras se realiza el examen del proceso de nuevo cifrado para una operación de cifrado de base de datos, las operaciones de mantenimiento de la base de datos están deshabilitadas.  
  
Puede encontrar el estado del cifrado de base de datos mediante la vista de administración dinámica **Sys. dm_pdw_nodes_database_encryption_keys** . Para obtener más información, vea la sección *vistas de catálogo y vistas de administración dinámica* anteriormente en este artículo.  
  
### <a name="restrictions"></a>Restricciones  
No se permiten las siguientes operaciones durante las `CREATE DATABASE ENCRYPTION KEY`instrucciones `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` .  
  
-   Eliminar la base de datos.  
  
-   Usar un `ALTER DATABASE` comando.  
  
-   Iniciar una copia de seguridad de base de datos.  
  
-   Iniciar una restauración de base de datos.  
  
Las operaciones o condiciones siguientes impedirán `CREATE DATABASE ENCRYPTION KEY`las `ALTER DATABASE ENCRYPTION KEY`instrucciones `DROP DATABASE ENCRYPTION KEY`,, `ALTER DATABASE...SET ENCRYPTION` o.  
  
-   Se `ALTER DATABASE` está ejecutando un comando.  
  
-   Se está ejecutando cualquier tipo de copia de seguridad de los datos.  
  
Al crear los archivos de base de datos, la inicialización instantánea de archivos no está disponible cuando TDE está habilitado.  
  
### <a name="areas-not-protected-by-tde"></a>Áreas no protegidas por TDE  
TDE no protege las tablas externas.  
  
TDE no protege las sesiones de diagnóstico. Los usuarios deben tener cuidado de no realizar consultas con parámetros confidenciales mientras se están usando sesiones de diagnóstico. Las sesiones de diagnóstico que revelen información confidencial deben quitarse en cuanto ya no se necesiten.  
  
Los datos protegidos por TDE se descifran cuando se colocan en PDW de SQL Server memoria. Los volcados de memoria se crean cuando se producen determinados problemas en el dispositivo. Los archivos de volcado representan el contenido de la memoria en el momento de la aparición del problema y pueden contener datos confidenciales en un formato no cifrado. El contenido de los volcados de memoria debe revisarse antes de que se compartan con otros usuarios.  
  
La base de datos maestra no está protegida por TDE. Aunque la base de datos maestra no contiene datos de usuario, contiene información como los nombres de inicio de sesión.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>El cifrado de datos transparente y los registros de transacciones  
Habilitar una base de datos para utilizar TDE tiene el efecto de poner en cero la parte restante del registro de transacciones virtual para forzar el siguiente registro de transacciones virtual. Esto garantiza que no quede ningún texto sin cifrar en los registros de transacciones una vez configurada la base de datos para el cifrado. Puede encontrar el estado del cifrado del archivo de registro en cada nodo de PDW mediante `encryption_state` la visualización de `sys.dm_pdw_nodes_database_encryption_keys` la columna en la vista, como en este ejemplo:  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
Todos los datos escritos en el registro de transacciones antes de cambiar la clave de cifrado de la base de datos se cifrarán mediante la clave de cifrado anterior de la base de datos.  
  
### <a name="pdw-activity-logs"></a>Registros de actividad de PDW  
PDW de SQL Server mantiene un conjunto de registros destinados a la solución de problemas. (Tenga en cuenta que no es el registro de transacciones, el registro de errores de SQL Server o el registro de eventos de Windows). Estos registros de actividad de PDW pueden contener instrucciones completas en texto no cifrado, algunas de las cuales pueden contener datos de usuario. Algunos ejemplos típicos son las instrucciones **Insert** y **Update** . El enmascaramiento de los datos de usuario se puede activar o desactivar explícitamente mediante **sp_pdw_log_user_data_masking**. Al habilitar el cifrado en PDW de SQL Server se activa automáticamente el enmascaramiento de los datos de usuario en los registros de actividad de PDW con el fin de protegerlos. **sp_pdw_log_user_data_masking** puede usarse también para enmascarar instrucciones cuando no se usa TDE, pero no se recomienda porque reduce significativamente la capacidad del equipo de soporte técnico de Microsoft de analizar los problemas.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>El cifrado de datos transparente y la base de datos del sistema tempdb  
La base de datos del sistema tempdb se cifra cuando se habilita el cifrado mediante [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Esto es necesario antes de que cualquier base de datos pueda usar TDE. Esto podría tener un efecto en el rendimiento de las bases de datos sin cifrar en la misma instancia de PDW de SQL Server.  
  
## <a name="key-management"></a>Administración de claves  
La clave de cifrado de base de datos (DEK) está protegida por los certificados almacenados en la base de datos maestra. Estos certificados están protegidos por la clave maestra de base de datos (DMK) de la base de datos maestra. El DMK debe estar protegido por la clave maestra de servicio (SMK) para que se pueda usar para TDE.  
  
El sistema puede acceder a las claves sin necesidad de intervención humana (por ejemplo, proporcionar una contraseña). Si el certificado no está disponible, el sistema generará un error que explica que el DEK no se puede descifrar hasta que el certificado adecuado esté disponible.  
  
Al mover una base de datos de un dispositivo a otro, el certificado que se usa para proteger su ' DEK debe restaurarse primero en el servidor de destino. A continuación, la base de datos se puede restaurar como de costumbre. Para obtener más información, consulte la documentación de SQL Server estándar, en el apartado sobre [Cómo trasladar una base de datos protegida por TDE a otra SQL Server](https://technet.microsoft.com/library/ff773063.aspx).  
  
Los certificados usados para cifrar DEK se deben conservar siempre que haya copias de seguridad de base de datos que las usen. Las copias de seguridad de certificados deben incluir la clave privada del certificado, ya que sin la clave privada, no se puede usar un certificado para restaurar la base de datos. Dichas copias de seguridad de claves privadas de certificados se almacenan en un archivo independiente, protegido por una contraseña que se debe proporcionar para la restauración de certificados.  
  
## <a name="restoring-the-master-database"></a>Restaurar la base de datos maestra  
La base de datos maestra se puede restaurar mediante **DWConfig**, como parte de la recuperación ante desastres.  
  
-   Si el nodo de control no ha cambiado, es decir, si la base de datos maestra se restaura en el mismo dispositivo y sin cambiar desde el que se tomó la copia de seguridad de la base de datos maestra, el DMK y todos los certificados se podrán leer sin ninguna acción adicional.  
  
-   Si la base de datos maestra se restaura en un dispositivo diferente, o si el nodo de control ha cambiado desde la copia de seguridad de la base de datos maestra, se necesitarán pasos adicionales para volver a generar el DMK.  
  
    1.  Abra DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Agregue el cifrado por SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Reinicie el dispositivo.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Actualizar y reemplazar Virtual Machines  
Si existe un DMK en el dispositivo en el que se realizó la actualización o la sustitución de la máquina virtual, se debe proporcionar la contraseña de DMK como parámetro.  
  
Ejemplo de la acción de actualización. Reemplace `**********` por la contraseña de DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
Ejemplo de la acción para reemplazar una máquina virtual.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
Durante la actualización, si una base de usuarios está cifrada y no se proporciona la contraseña de DMK, se producirá un error en la acción de actualización. Durante el reemplazo, si no se proporciona la contraseña correcta cuando existe un DMK, la operación omitirá el paso de recuperación de DMK. Todos los demás pasos se completarán al final de la acción reemplazar VM, pero la acción informará de un error al final para indicar que se requieren pasos adicionales. En los registros de instalación (que se encuentran en **\ProgramData\Microsoft\Microsoft SQL Server\\ Warehouse\100\Logs\Setup de datos paralelos<marca de tiempo> \detail-Setup**), se mostrará la siguiente advertencia cerca del final.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
Ejecute estas instrucciones manualmente en PDW y reinicie el dispositivo después de eso para recuperar DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Siga los pasos descritos en el párrafo **restaurar la base de datos maestra** para recuperar la base de datos y, a continuación, reinicie el dispositivo.  
  
Si el DMK existía antes pero no se recuperó después de la acción, se generará el siguiente mensaje de error cuando se consulte una base de datos.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impacto en el rendimiento  
El impacto en el rendimiento de TDE varía con el tipo de datos que tiene, la forma en que se almacena y el tipo de actividad de la carga de trabajo en el PDW de SQL Server. Cuando está protegido por TDE, la e/s de lectura y descifrado de datos o el cifrado y, después, la escritura de datos, es una actividad con un uso intensivo de la CPU y tendrá más impacto cuando se produzcan otras actividades intensivas de CPU al mismo tiempo. Dado que TDE cifra `tempdb`, TDE puede afectar al rendimiento de las bases de datos que no están cifradas. Para obtener una idea precisa del rendimiento, debe probar todo el sistema con los datos y la actividad de la consulta.  
  
## <a name="related-content"></a>Contenido relacionado  
Los vínculos siguientes contienen información general acerca de cómo SQL Server administra el cifrado. Estos artículos pueden ayudarle a comprender el cifrado de SQL Server, pero estos artículos no tienen información específica de PDW de SQL Server y describen las características que no están presentes en PDW de SQL Server.  
  
-   [Cifrado de SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Jerarquía de cifrado](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server y claves de cifrado de base de datos](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Consulte también  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)  
[CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
