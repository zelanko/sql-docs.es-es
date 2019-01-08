---
title: Cifrado de datos transparente - almacenamiento de datos paralelos | Microsoft Docs
description: Cifrado de datos transparente (TDE) para el almacenamiento de datos paralelos (PDW) realiza el cifrado de E/S en tiempo real y descifrado de los datos y archivos de registro de transacciones y los archivos de registro PDW especiales."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea15a8fc5eaf066b5a64cf73192f64dd0078434e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534078"
---
# <a name="transparent-data-encryption"></a>Cifrado de datos transparente
Puede tomar varias precauciones para proteger la base de datos, como diseñar un sistema seguro, cifrar los datos confidenciales e instalar un firewall alrededor de los servidores de bases de datos. Sin embargo, para un escenario en el que se roban medios físicos (como unidades o cintas de copia de seguridad), un tercero malintencionado puede simplemente restaurar o adjuntar la base de datos y examinar los datos. Una solución consiste en cifrar los datos confidenciales en la base de datos y usar un certificado para proteger las claves que se utilizan para cifrarlos. Esto evita que utilice los datos cualquiera que carezca de las claves, pero este tipo de protección debe planearse de antemano.  
  
*Cifrado de datos transparente* (TDE) realiza el cifrado de E/S en tiempo real y el descifrado de los datos y los archivos de registro de archivos de registro de transacciones y PDW especial. El cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. La DEK es una clave simétrica protegida utilizando un certificado almacenado en la base de datos maestra de SQL Server PDW. TDE protege los datos "en reposo", es decir, los archivos de datos y de registro. Ofrece la posibilidad de cumplir muchas leyes, normativas y directrices establecidas en diversos sectores. Esta característica permite a los desarrolladores de software cifrar los datos mediante el uso de algoritmos de cifrado AES y 3DES sin cambiar las aplicaciones existentes.  
  
> [!IMPORTANT]  
> TDE no proporciona cifrado de datos que se desplazan entre el cliente y PDW. Para obtener más información acerca de cómo cifrar los datos entre el cliente y SQL Server PDW, vea [aprovisionar un certificado](provision-certificate.md).  
>   
> TDE no cifra los datos mientras se mueve o se encuentra en uso. No se cifra el tráfico interno entre los componentes PDW dentro de PDW de SQL Server. No se cifran los datos almacenados temporalmente en los búferes de memoria. Para mitigar este riesgo, controlar el acceso físico y las conexiones con PDW de SQL Server.  
  
Una vez protegida, la base de datos puede restaurarse utilizando el certificado correcto.  
  
> [!NOTE]  
> Cuando se crea un certificado para TDE, debe hacerla inmediatamente, junto con la clave privada asociada. Si el certificado no está disponible en algún momento o si debe restaurar o adjuntar la base de datos en otro servidor, debe tener copias de seguridad del certificado y la clave privada o no podrá abrir la base de datos. El cifrado del certificado se debería conservar aun cuando TDE deje de estar habilitado en la base de datos. Aunque la base de datos no se cifre, algunas partes del registro de transacciones pueden seguir estando protegidas y se puede necesitar el certificado para algunas operaciones hasta que se realice la copia de seguridad completa de la base de datos. Un certificado que ha excedido su fecha de expiración se puede seguir usando para cifrar y descifrar datos con TDE.  
  
El cifrado del archivo de base de datos se realiza en el nivel de página. Las páginas de una base de datos cifrada se cifran antes de escribirse en el disco y se descifran cuando se leen en la memoria. TDE no aumenta el tamaño de la base de datos cifrada.  
  
La siguiente ilustración muestra la jerarquía de claves de cifrado de TDE:  
  
![Muestra la jerarquía](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Uso del cifrado de datos transparente  
Para usar TDE, siga estos pasos. Los tres primeros pasos solo se realizan una vez, al preparar PDW de SQL Server para admitir TDE.  
  
1.  Cree una clave maestra de base de datos maestra.  
  
2.  Use **sp_pdw_database_encryption para** para habilitar TDE en el PDW de SQL Server. Esta operación modifica las bases de datos temporales con el fin de garantizar la protección de datos temporales futuros y se producirá un error si intenta cuando hay las sesiones activas que tienen tablas temporales. **sp_pdw_database_encryption para** activa el enmascaramiento de datos de usuario en los registros del sistema PDW. (Para obtener más información acerca de enmascaramiento de datos de usuario en los registros del sistema PDW, vea [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Use [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) para crear una credencial que pueda autenticar y escribir en el recurso compartido donde se almacenará la copia de seguridad del certificado. Si ya existe una credencial para el servidor de almacenamiento previsto, puede usar la credencial existente.  
  
4.  En la base de datos maestra, crear un certificado protegido por la clave maestra.  
  
5.  Copia de seguridad del certificado en el recurso compartido de almacenamiento.  
  
6.  En la base de datos de usuario, cree una clave de cifrado de base de datos y protéjala con el certificado que se almacena en la base de datos maestra.  
  
7.  Use el `ALTER DATABASE` instrucción para cifrar la base de datos mediante TDE.  
  
El siguiente ejemplo ilustra cifrar el `AdventureWorksPDW2012` base de datos mediante un certificado denominado `MyServerCert`, creado en PDW de SQL Server.  
  
**En primer lugar: Habilitar TDE en SQL Server PDW.** Esta acción solo es necesaria una vez.  
  
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
  
**Segundo: Cree y un certificado en la base de datos maestra de copia de seguridad.** Esta acción solo es necesaria una vez. Puede tener un certificado independiente para cada base de datos (recomendado) o puede proteger varias bases de datos con un certificado.  
  
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
  
**Último: Cree la clave DEK y utilice ALTER DATABASE para cifrar una base de datos de usuario.** Esta acción se repite para cada base de datos protegida por TDE.  
  
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
  
Se programan las operaciones de cifrado y descifrado en subprocesos en segundo plano por SQL Server. Puede ver el estado de estas operaciones mediante las vistas de catálogo y vistas de administración dinámica de la lista que aparece más adelante en este artículo.  
  
> [!CAUTION]  
> Los archivos de copia de seguridad de las bases de datos que tienen habilitado TDE también se cifran mediante la clave de cifrado de la base de datos. Como consecuencia, al restaurar estas copias de seguridad debe estar disponible el certificado que protege la clave de cifrado de la base de datos. Esto significa que, además de hacer copias de seguridad de la base de datos, tiene que asegurarse de que mantiene copias de seguridad de los certificados del servidor para evitar la pérdida de datos. Si el certificado deja de estar disponible, perderá los datos.  
  
## <a name="commands-and-functions"></a>Comandos y funciones  
Para que puedan ser aceptados por las instrucciones siguientes, los certificados de TDE deben cifrarse con la clave maestra de la base de datos.  
  
En la tabla siguiente se proporcionan vínculos y explicaciones de los comandos y funciones de TDE.  
  
|Comando o función|Propósito|  
|-----------------------|-----------|  
|[CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Crea una clave que se utiliza para cifrar una base de datos.|  
|[MODIFICAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Cambia la clave que se utiliza para cifrar una base de datos.|  
|[DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Quita la clave que se utilizó para cifrar una base de datos.|  
|[MODIFICAR BASE DE DATOS](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Explica la opción **ALTER DATABASE** que se utiliza para habilitar TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Vistas de catálogo y vistas de administración dinámica  
En la tabla siguiente se muestran las vistas de catálogo y las vistas de administración dinámica de TDE.  
  
|Vista de catálogo o vista de administración dinámica|Propósito|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista de catálogo que muestra información sobre las bases de datos.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista de catálogo que muestra los certificados de una base de datos.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Vista de administración dinámica que proporciona información para cada nodo, acerca de las claves de cifrado utilizado en una base de datos y el estado de cifrado de una base de datos.|  
  
## <a name="permissions"></a>Permisos  
Cada una de las características y comandos de TDE tiene sus propios requisitos de permisos, que se describen en las tablas mostradas anteriormente.  
  
Ver los metadatos relacionados con TDE, se requiere el `CONTROL SERVER` permiso.  
  
## <a name="considerations"></a>Consideraciones  
Mientras se realiza el examen del proceso de nuevo cifrado para una operación de cifrado de base de datos, las operaciones de mantenimiento de la base de datos están deshabilitadas.  
  
Puede encontrar el estado de la base de datos de cifrado mediante la **sys.dm_pdw_nodes_database_encryption_keys** vista de administración dinámica. Para obtener más información, consulte el *vistas de catálogo y vistas de administración dinámica* anteriormente en este artículo.  
  
### <a name="restrictions"></a>Restrictions  
No se permiten las operaciones siguientes durante el `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` instrucciones.  
  
-   Eliminar la base de datos.  
  
-   Mediante un `ALTER DATABASE` comando.  
  
-   A partir de una copia de seguridad de base de datos.  
  
-   A partir de una restauración de base de datos.  
  
Las siguientes operaciones o condiciones impedirá la `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` instrucciones.  
  
-   Un `ALTER DATABASE` ejecutando el comando.  
  
-   Se está ejecutando cualquier tipo de copia de seguridad de los datos.  
  
Al crear los archivos de base de datos, la inicialización instantánea de archivos no está disponible cuando TDE está habilitado.  
  
### <a name="areas-not-protected-by-tde"></a>Áreas no protegidas por TDE  
TDE no protege las tablas externas.  
  
TDE no protege las sesiones de diagnóstico. Los usuarios deben tener cuidados no a las consultas con parámetros confidenciales mientras sesiones de diagnóstico están en uso. En cuanto ya no son necesarios, se deben quitar las sesiones de diagnóstico que revelen información confidencial.  
  
Datos protegidos por TDE se descifran cuando se coloca en la memoria de SQL Server PDW. Los volcados de memoria se crean cuando se producen ciertos problemas en el dispositivo. Archivos representan el contenido de la memoria en el momento de la apariencia del problema de volcado de memoria y puede contener datos confidenciales sin cifrar. El contenido de los volcados de memoria debe revisarse antes de que se comparten con otros usuarios.  
  
La base de datos maestra no está protegida por TDE. Aunque la base de datos maestra no contiene datos de usuario, lo que contienen información como nombres de inicio de sesión.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>El cifrado de datos transparente y los registros de transacciones  
Habilitación de una base de datos utilizar TDE tiene el efecto de la parte restante del registro de transacciones virtual para forzar el registro de transacciones virtual siguiente pone a cero. Esto garantiza que no quede ningún texto sin cifrar en los registros de transacciones una vez configurada la base de datos para el cifrado. Puede encontrar el estado de cifrado de archivos de registro en cada nodo PDW observando el `encryption_state` columna en la `sys.dm_pdw_nodes_database_encryption_keys` vista, como en este ejemplo:  
  
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
  
### <a name="pdw-activity-logs"></a>Registros de actividad PDW  
PDW de SQL Server mantiene un conjunto de registros diseñado para solucionar problemas. (Observe que esto no es el registro de transacciones, el registro de errores de SQL Server o el registro de eventos de Windows). Estos registros de actividad PDW pueden contener instrucciones completas en texto no cifrado, algunos de los cuales pueden contener datos de usuario. Ejemplos típicos son **insertar** y **actualización** instrucciones. Enmascaramiento de datos de usuario puede ser explícitamente activar o desactivar mediante el uso de **sp_pdw_log_user_data_masking**. Habilitación del cifrado en SQL Server PDW automáticamente activa el enmascaramiento de datos de usuario en los registros de actividad PDW para protegerlos. **sp_pdw_log_user_data_masking** también se puede usar para enmascarar las instrucciones cuando no se usa TDE, pero que no se recomienda porque reduce significativamente la posibilidad de que el equipo de soporte técnico de Microsoft para analizar los problemas.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>El cifrado de datos transparente y la base de datos del sistema tempdb  
La base de datos del sistema tempdb se cifra cuando se habilita el cifrado mediante el uso de [sp_pdw_database_encryption para](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Esto es necesario para cualquier base de datos puede usar TDE. Esto podría tener un efecto de rendimiento para bases de datos sin cifrar en la misma instancia de SQL Server PDW.  
  
## <a name="key-management"></a>Administración de claves  
La clave de cifrado de base de datos (DEK) está protegida por los certificados almacenados en la base de datos maestra. Estos certificados están protegidos por la clave maestra de base de datos (DMK) de la base de datos maestra. La DMK debe protegerse mediante la clave maestra de servicio (SMK) para poder usarlo para TDE.  
  
El sistema puede tener acceso a las claves sin intervención del usuario (por ejemplo, para proporcionar una contraseña). Si el certificado no está disponible, el sistema generará un error que indicará que no se puede descifrar la DEK hasta que el certificado correcto esté disponible.  
  
Al mover una base de datos de un dispositivo a otro, el certificado se usa para proteger su ' DEK primero debe restaurarse en el servidor de destino. A continuación, la base de datos puede restaurarse como de costumbre. Para obtener más información, consulte la documentación de SQL Server estándar, en [mover una base de datos protegida de TDE a otra de SQL Server](https://technet.microsoft.com/library/ff773063.aspx).  
  
Los certificados usados para cifrar la DEK se deben conservar, siempre hay copias de seguridad de base de datos que los usan. Las copias de seguridad del certificado deben incluir la clave privada del certificado, porque sin la clave privada no se puede usar un certificado para la restauración de base de datos. Las copias de seguridad de clave privada de certificado se almacenan en un archivo independiente, protegido mediante contraseña que se debe proporcionar para la restauración de certificado.  
  
## <a name="restoring-the-master-database"></a>Restaurar la base de datos master  
Se puede restaurar la base de datos maestra mediante **DWConfig**, como parte de la recuperación ante desastres.  
  
-   Si no ha cambiado el nodo de control, que es que si se restaura la base de datos maestra en el dispositivo mismo y sin cambios desde que se ha realizado la copia de seguridad de base de datos maestra, todos los certificados y la DMK serán legibles sin ninguna acción adicional.  
  
-   Si la base de datos principal se restaura en otro dispositivo, o si el nodo de control ha cambiado desde la copia de seguridad de la base de datos maestra, deberán pasos adicionales para volver a generar la DMK.  
  
    1.  Abra la DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Agregue el cifrado mediante la SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Reinicie el dispositivo.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Actualización y reemplazar las máquinas virtuales  
Si existe una DMK en el dispositivo en el que se realizó la actualización o reemplazar VM, debe proporcionarse la contraseña DMK como un parámetro.  
  
Ejemplo de la acción de actualización. Reemplace `**********` con la contraseña de la DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'  `  
  
Ejemplo de la acción que se va a reemplazar una máquina virtual.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'  `  
  
Durante la actualización, si un usuario de base de datos se cifran y no se proporciona la contraseña de la DMK, la acción de actualización se producirá un error. Durante el reemplazo, si no se proporciona la contraseña correcta cuando existe una DMK, la operación omitirá el paso de recuperación de la DMK. Todos los demás pasos se completará al final de la acción de máquina virtual de reemplazo, sin embargo, la acción notificará un error al final para indicar que se requieren pasos adicionales. En los registros de instalación (ubicado en **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\\Detail-Setup < marca de tiempo >**), se mostrará la siguiente advertencia cerca del final.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!  `
  
Ejecute estas instrucción manualmente en PDW y reinicie el dispositivo después de con el fin de recuperar la DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Siga los pasos de la **restaurar la base de datos maestra** párrafo para recuperar la base de datos y, a continuación, reinicie el dispositivo.  
  
Si la DMK existía antes, pero no se ha recuperado después de la acción, se producirá el siguiente mensaje de error cuando se consulta una base de datos.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impacto sobre el rendimiento  
El impacto de rendimiento de TDE varía según el tipo de datos que tiene, cómo se almacenan y el tipo de actividad de carga de trabajo en el PDW de SQL Server. Cuando protegida por TDE, la E/S de lectura y descifrar los datos o el cifrado y, a continuación, escribir datos es una actividad de uso intensivo de CPU y tendrán mayor impacto cuando se producen otras actividades de uso intensivo de CPU al mismo tiempo. Dado que el TDE cifra `tempdb`, TDE puede afectar al rendimiento de bases de datos que no estén cifrados. Para obtener una idea precisa de rendimiento, debe probar todo el sistema con la actividad de datos y la consulta.  
  
## <a name="related-content"></a>Contenido relacionado  
Los vínculos siguientes contienen información general acerca de cómo SQL Server administra el cifrado. Estos artículos pueden ayudarle a entender el cifrado de SQL Server, pero estos artículos no tienen información específica de PDW de SQL Server y se describen las características que no están presentes en PDW de SQL Server.  
  
-   [Cifrado de SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Jerarquía de cifrado](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server y claves de cifrado de la base de datos](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Vea también  
[MODIFICAR BASE DE DATOS](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CREAR LA CLAVE MAESTRA](../t-sql/statements/create-master-key-transact-sql.md)  
[CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
