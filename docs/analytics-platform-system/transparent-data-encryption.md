---
title: 'Cifrado de datos transparente: almacenamiento de datos paralelos | Documentos de Microsoft'
description: Cifrado de datos transparente (TDE) para el almacenamiento de datos paralelo (PDW) realiza el cifrado de E/S en tiempo real y el descifrado de los datos y archivos de registro de transacciones y los archivos de registro PDW especiales."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6dc8bef420939d64b569ae285e6a3525d57983bd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="transparent-data-encryption"></a>Cifrado de datos transparente
Puede tomar varias precauciones para proteger la base de datos, como diseñar un sistema seguro, cifrar los datos confidenciales e instalar un firewall alrededor de los servidores de bases de datos. Sin embargo, para un escenario en el que se diera el caso de los medios físicos (por ejemplo, unidades de disco o cintas de copia de seguridad), un tercero malintencionado puede restaurar o adjuntar la base de datos y examinar los datos. Una solución consiste en cifrar los datos confidenciales en la base de datos y usar un certificado para proteger las claves que se utilizan para cifrarlos. Esto evita que utilice los datos cualquiera que carezca de las claves, pero este tipo de protección debe planearse de antemano.  
  
*Cifrado de datos transparente* (TDE) realiza el cifrado de E/S en tiempo real y el descifrado de los datos y archivos de registro de archivos de registro de transacciones y PDW especial. El cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. La DEK es una clave simétrica protegida utilizando un certificado almacenado en la base de datos maestra de SQL Server PDW. TDE protege los datos "en reposo", es decir, los archivos de datos y de registro. Ofrece la posibilidad de cumplir muchas leyes, normativas y directrices establecidas en diversos sectores. Esta característica permite a los desarrolladores de software cifrar los datos mediante el uso de algoritmos de cifrado AES y 3DES sin cambiar las aplicaciones existentes.  
  
> [!IMPORTANT]  
> TDE no proporciona cifrado de datos que se desplazan entre el cliente y el PDW. Para obtener más información acerca de cómo cifrar los datos entre el cliente y SQL Server PDW, vea [aprovisionar un certificado](provision-certificate.md).  
>   
> TDE no cifra los datos mientras se mueve o está en uso. No se cifra el tráfico interno entre los componentes PDW dentro de SQL Server PDW. No se cifran los datos que se almacenan temporalmente en búferes de memoria. Para mitigar este riesgo, controlar el acceso físico y las conexiones a SQL Server PDW.  
  
Una vez protegida, la base de datos puede restaurarse utilizando el certificado correcto.  
  
> [!NOTE]  
> Cuando se crea un certificado para TDE, debe hacerla inmediatamente, junto con la clave privada asociada. Si el certificado no está disponible en algún momento o si debe restaurar o adjuntar la base de datos en otro servidor, debe tener copias de seguridad del certificado y la clave privada o no podrá abrir la base de datos. El cifrado del certificado se debería conservar aun cuando TDE deje de estar habilitado en la base de datos. Aunque la base de datos no se cifre, algunas partes del registro de transacciones pueden seguir estando protegidas y se puede necesitar el certificado para algunas operaciones hasta que se realice la copia de seguridad completa de la base de datos. Un certificado que ha excedido su fecha de expiración se puede seguir usando para cifrar y descifrar datos con TDE.  
  
El cifrado del archivo de base de datos se realiza en el nivel de página. Las páginas de una base de datos cifrada se cifran antes de escribirse en el disco y se descifran cuando se leen en la memoria. TDE no aumenta el tamaño de la base de datos cifrada.  
  
En la siguiente ilustración muestra la jerarquía de claves de cifrado de TDE:  
  
![Muestra la jerarquía](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Mediante el cifrado de datos transparente  
Para usar TDE, siga estos pasos. Los tres primeros pasos solo se realizan una vez, cuando se prepara PDW de SQL Server para admitir TDE.  
  
1.  Cree una clave maestra de la base de datos maestra.  
  
2.  Use **sp_pdw_database_encryption** para habilitar TDE en SQL Server PDW. Esta operación modifica las bases de datos temporales con el fin de garantizar la protección de datos temporales en el futuro y se producirá un error si intenta cuando hay alguna sesión activa que tienen tablas temporales. **sp_pdw_database_encryption** activa el enmascaramiento de datos de usuario en los registros de sistema PDW. (Para obtener más información acerca de enmascaramiento de datos de usuario en los registros de sistema PDW, vea [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Use [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) para crear una credencial que pueda autenticar y escribir en el recurso compartido donde se almacenará la copia de seguridad del certificado. Si ya existe una credencial para el servidor de almacenamiento previsto, puede usar la credencial existente.  
  
4.  En la base de datos maestra, cree un certificado protegido por la clave maestra.  
  
5.  Copia de seguridad del certificado para el recurso compartido de almacenamiento.  
  
6.  En la base de datos de usuario, cree una clave de cifrado de base de datos y protéjala con el certificado que se almacena en la base de datos maestra.  
  
7.  Use la `ALTER DATABASE` instrucción para cifrar la base de datos mediante TDE.  
  
En el ejemplo siguiente se ilustra el cifrado de la `AdventureWorksPDW2012` mediante un certificado con el nombre de la base de datos `MyServerCert`, creado en SQL Server PDW.  
  
**Primero: Habilitar TDE en SQL Server PDW.** Esta acción solo es necesaria una vez.  
  
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
  
**Segundo: Crear y copia de seguridad de un certificado en la base de datos maestra.** Esta acción solo es necesario una vez. Puede tener un certificado independiente para cada base de datos (recomendado), o puede proteger varias bases de datos con un certificado.  
  
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
  
**Última: Crear la DEK y utilice ALTER DATABASE para cifrar una base de datos de usuario.** Esta acción se repite para cada base de datos está protegida por TDE.  
  
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
  
El programa de las operaciones de cifrado y descifrado se ejecutan en subprocesos en segundo plano, con SQL Server. Puede ver el estado de estas operaciones mediante las vistas de catálogo y vistas de administración dinámica de la lista que aparece más adelante en este artículo.  
  
> [!CAUTION]  
> Los archivos de copia de seguridad de las bases de datos que tienen habilitado TDE también se cifran mediante la clave de cifrado de la base de datos. Como consecuencia, al restaurar estas copias de seguridad debe estar disponible el certificado que protege la clave de cifrado de la base de datos. Esto significa que, además de hacer copias de seguridad de la base de datos, tiene que asegurarse de que mantiene copias de seguridad de los certificados del servidor para evitar la pérdida de datos. Si el certificado deja de estar disponible, perderá los datos.  
  
## <a name="commands-and-functions"></a>Comandos y funciones  
Para que puedan ser aceptados por las instrucciones siguientes, los certificados de TDE deben cifrarse con la clave maestra de la base de datos.  
  
En la tabla siguiente se proporcionan vínculos y explicaciones de los comandos y funciones de TDE.  
  
|Comando o función|Finalidad|  
|-----------------------|-----------|  
|[CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Crea una clave que se utiliza para cifrar una base de datos.|  
|[MODIFICAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Cambia la clave que se utiliza para cifrar una base de datos.|  
|[QUITAR LA CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Quita la clave que se utilizó para cifrar una base de datos.|  
|[MODIFICAR BASE DE DATOS](../t-sql/statements/alter-database-parallel-data-warehouse.md)|Explica la opción **ALTER DATABASE** que se utiliza para habilitar TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Vistas de catálogo y vistas de administración dinámica  
En la tabla siguiente se muestran las vistas de catálogo y las vistas de administración dinámica de TDE.  
  
|Vista de catálogo o vista de administración dinámica|Finalidad|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista de catálogo que muestra información sobre las bases de datos.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista de catálogo que muestra los certificados de una base de datos.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Vista de administración dinámica que proporciona información para cada nodo, acerca de las claves de cifrado utilizadas en una base de datos y el estado de cifrado de una base de datos.|  
  
## <a name="permissions"></a>Permissions  
Cada una de las características y comandos de TDE tiene sus propios requisitos de permisos, que se describen en las tablas mostradas anteriormente.  
  
Ver los metadatos relacionados con TDE, se requiere el `CONTROL SERVER` permiso.  
  
## <a name="considerations"></a>Consideraciones  
Mientras se realiza el examen del proceso de nuevo cifrado para una operación de cifrado de base de datos, las operaciones de mantenimiento de la base de datos están deshabilitadas.  
  
Puede encontrar el estado de la base de datos de cifrado mediante la **sys.dm_pdw_nodes_database_encryption_keys** vista de administración dinámica. Para obtener más información, consulte el *vistas de catálogo y vistas de administración dinámica* sección anteriormente en este artículo.  
  
### <a name="restrictions"></a>Restricciones  
Las siguientes operaciones no están permitidas durante la `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` las instrucciones.  
  
-   Eliminar la base de datos.  
  
-   Mediante un `ALTER DATABASE` comando.  
  
-   A partir de una copia de seguridad de base de datos.  
  
-   A partir de una restauración de base de datos.  
  
Las operaciones o condiciones siguientes impedirán la `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, o `ALTER DATABASE...SET ENCRYPTION` las instrucciones.  
  
-   Un `ALTER DATABASE` ejecutando el comando.  
  
-   Se está ejecutando cualquier tipo de copia de seguridad de los datos.  
  
Al crear los archivos de base de datos, la inicialización instantánea de archivos no está disponible cuando TDE está habilitado.  
  
### <a name="areas-not-protected-by-tde"></a>Áreas no protegidas por TDE  
TDE no protege las tablas externas.  
  
TDE no protege sesiones de diagnóstico. Los usuarios deben tener cuidadosos de no a las consultas con parámetros confidenciales mientras sesiones de diagnóstico están en uso. Sesiones de diagnóstico que revelan información confidencial se deben quitar tan pronto como ya no son necesarios.  
  
Cuando se coloca en la memoria de SQL Server PDW, se descifran los datos protegidos por TDE. Volcados de memoria se crean cuando se producen ciertos problemas en el dispositivo. Volcar archivos representan el contenido de la memoria en el momento de la apariencia del problema y puede contener datos confidenciales en un formato sin cifrar. El contenido de volcados de memoria debe revisarse antes de que se comparten con otros usuarios.  
  
La base de datos maestra no está protegida por TDE. Aunque la base de datos maestra no contiene datos de usuario, lo que contienen información como los nombres de inicio de sesión.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>El cifrado de datos transparente y los registros de transacciones  
Habilitar una base de datos utilizar TDE tiene el efecto de pone a cero la parte restante del registro de transacciones virtual para exigir el registro de transacciones virtual siguiente. Esto garantiza que no quede ningún texto sin cifrar en los registros de transacciones una vez configurada la base de datos para el cifrado. Puede encontrar el estado de cifrado de archivos de registro en cada nodo PDW observando el `encryption_state` columna en la `sys.dm_pdw_nodes_database_encryption_keys` vista, como en este ejemplo:  
  
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
PDW de SQL Server mantiene un conjunto de registros diseñados para solucionar problemas. (Observe que esto no es el registro de transacciones, el registro de errores de SQL Server o el registro de eventos de Windows). Estos registros de actividad PDW pueden contener instrucciones completas en texto no cifrado, algunos de los cuales pueden contener datos de usuario. Ejemplos típicos son **insertar** y **actualización** instrucciones. Enmascaramiento de datos de usuario puede ser explícitamente activado o desactivada mediante el uso de **sp_pdw_log_user_data_masking**. Habilitar el cifrado en SQL Server PDW automáticamente activa el enmascaramiento de datos del usuario en los registros de actividad PDW para protegerlos. **sp_pdw_log_user_data_masking** también puede utilizarse para enmascarar las instrucciones al no utilizar TDE, pero que no se recomienda porque reduce significativamente la posibilidad de que el equipo de soporte técnico de Microsoft para analizar los problemas.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>El cifrado de datos transparente y la base de datos del sistema tempdb  
La base de datos del sistema tempdb se cifra cuando está habilitado el cifrado mediante el uso de [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Esto es necesario para cualquier base de datos puede usar TDE. Esto podría tener un efecto de rendimiento para bases de datos sin cifrar en la misma instancia de SQL Server PDW.  
  
## <a name="key-management"></a>Administración de claves  
La clave de cifrado de base de datos (DEK) está protegida por los certificados almacenados en la base de datos maestra. Estos certificados se protegen mediante la clave maestra de base de datos (DMK) de la base de datos maestra. La DMK necesita ser protegido mediante la clave maestra de servicio (SMK) para poder usarlo para TDE.  
  
El sistema puede tener acceso a las claves sin necesidad de intervención humana (por ejemplo, para proporcionar una contraseña). Si el certificado no está disponible, el sistema dará como resultado un error que indicará que no se puede descifrar la DEK hasta que esté disponible el certificado adecuado.  
  
Al mover una base de datos de un dispositivo a otro, el certificado se utiliza para proteger su ' DEK primero debe restaurarse en el servidor de destino. A continuación, la base de datos puede restaurarse como de costumbre. Para obtener más información, consulte la documentación de SQL Server estándar, en [mover una base de datos protegida de TDE a otro servidor SQL Server](http://technet.microsoft.com/library/ff773063.aspx).  
  
Certificados utilizados para cifrar la DEK deben conservarse mientras hay copias de seguridad de base de datos que las utilizan. Las copias de seguridad del certificado deben incluir la clave privada del certificado, porque sin la clave privada no se puede usar un certificado para la restauración de base de datos. Las copias de seguridad de clave privada de certificado se almacenan en un archivo independiente, protegido mediante contraseña que se debe proporcionar para la restauración de certificado.  
  
## <a name="restoring-the-master-database"></a>Restaurar la base de datos master  
La base de datos maestra se puede restaurar utilizando **DWConfig**, como parte de la recuperación ante desastres.  
  
-   Si no ha cambiado el nodo de control, que es que si se restaura la base de datos maestra en el dispositivo mismo y sin cambios desde la que se realizó la copia de seguridad de base de datos maestra, la DMK y todos los certificados se podrán leer sin ninguna acción adicional.  
  
-   Si la base de datos principal se restaura en otro dispositivo, o si el nodo de control ha cambiado desde la copia de seguridad de la base de datos maestra, se requerirá pasos adicionales para volver a generar la DMK.  
  
    1.  Abra la DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Agregue el cifrado de SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Reinicie el dispositivo.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Actualización y reemplazando las máquinas virtuales  
Si existe una DMK en el dispositivo en el que se realizó la actualización o reemplazar VM, debe proporcionarse la contraseña de base como parámetro.  
  
Ejemplo de la acción de actualización. Reemplace `**********` con la contraseña de la DMK.  
  
`setup.exe /Action=ProvisionUpgrade … DMKPassword='**********'  `  
  
Ejemplo de la acción que se va a reemplazar una máquina virtual.  
  
`setup.exe /Action=ReplaceVM … DMKPassword='**********'  `  
  
Durante la actualización, si se cifra un base de datos de usuario y la contraseña de base no se proporciona, la acción de actualización se producirá un error. Durante el reemplazo, si no se proporciona la contraseña correcta cuando existe una DMK, la operación lo omitirá el paso de recuperación de base. Todos los demás pasos se completarán al final de la acción de VM replace, sin embargo, la acción va a notificar errores al final para indicar que se requieren pasos adicionales. En los registros de instalación (ubicado en **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\\Detail-Setup < hora >**), se mostrará la siguiente advertencia cerca del final.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!  `
  
Ejecute estos instrucción manualmente en PDW y reiniciar el dispositivo después de con el fin de recuperar la base:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Siga los pasos de la **restaurar la base de datos maestra** apartado para recuperar la base de datos y, a continuación, reinicie el dispositivo.  
  
Si la DMK existía antes, pero no se ha recuperado después de la acción, se generará el siguiente mensaje de error cuando se consulta una base de datos.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impacto sobre el rendimiento  
El impacto en el rendimiento de TDE varía según el tipo de datos, cómo se almacena y el tipo de actividad de carga de trabajo de SQL Server PDW. Cuando protegida por TDE, la E/S de lectura y, a continuación, descifrar los datos o el cifrado y, a continuación, escribir datos es una actividad de uso intensivo de CPU y tiene más efecto cuando se producen otras actividades de uso intensivo de CPU al mismo tiempo. Dado que TDE cifra `tempdb`, TDE puede afectar al rendimiento de las bases de datos que no estén cifrados. Para obtener una idea exacta de rendimiento, debe probar todo el sistema con la actividad de consultas y los datos.  
  
## <a name="related-content"></a>Contenido relacionado  
Los vínculos siguientes contienen información general acerca de cómo SQL Server administra el cifrado. Estos artículos pueden ayudarle a entender el cifrado de SQL Server, pero estos artículos no tienen información específica de PDW de SQL Server y describen las características que no están presentes en PDW de SQL Server.  
  
-   [Cifrado de SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Jerarquía de cifrado](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [SQL Server y claves de cifrado de la base de datos](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Vea también  
[MODIFICAR BASE DE DATOS](../t-sql/statements/alter-database-parallel-data-warehouse.md)  
[CREAR LA CLAVE MAESTRA](../t-sql/statements/create-master-key-transact-sql.md)  
[CREAR CLAVE DE CIFRADO DE BASE DE DATOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
