---
title: Actualización de una base de datos mediante Separar y Adjuntar (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 11/26/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e26f678ae13fac11c39569d15e26c0e79e46deb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74095537"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>Actualización de una base de datos mediante Separar y Adjuntar (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En este tema se describe cómo usar las operaciones de separar y adjuntar para actualizar una base de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Después de asociarla a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos está disponible de inmediato y se actualiza automáticamente. Esto evita que la base de datos se use con una versión anterior de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Pero la actualización de metadatos no afecta al valor de [nivel de compatibilidad de base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) de una base de datos. Obtenga más información en [Nivel de compatibilidad de la base de datos después de la actualización](#dbcompat) más adelante en este tema.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para actualizar una base de datos de SQL Server:**  
  
     [Usando operaciones de separar y adjuntar](#SSMSProcedure)  
  
-   **Seguimiento:**    

     [Después de actualizar una base de datos de SQL Server](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las bases de datos del sistema no pueden adjuntarse.  
  
-   Las operaciones de adjuntar y separar deshabilitan el encadenamiento de propiedad entre bases de datos si se establece la opción **cross db ownership chaining** en 0. Para obtener más información sobre cómo habilitar el encadenamiento, vea [cross db ownership chaining (opción de configuración del servidor)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
-   Cuando adjunte una base de datos replicada que fue copiada en lugar de separada:  
  
    -   Si se adjunta la base de datos a una versión actualizada de la misma instancia de servidor, es necesario ejecutar **sp_vupgrade_replication** para actualizar la replicación una vez finalizada la operación de adjuntar. Para obtener más información, vea [sp_vupgrade_replication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md).  
  
    -   Si adjunta la base de datos a una instancia de servidor diferente, sin que importe la versión, debe ejecutar **sp_removedbreplication** para quitar la replicación una vez completada la operación de adjuntar. Para obtener más información, vea [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Para actualizar una base de datos mediante las operaciones de separar y adjuntar  
  
1.  Separe la base de datos. Para obtener más información, vea [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
2.  También puede mover los archivos de la base de datos separada y los archivos de registro.  
  
     Debe mover los archivos de registro, junto con los archivos de datos, incluso aunque piense crear archivos de registro. En algunos casos, para volver a adjuntar una base de datos son necesarios sus archivos de registro. Por tanto, mantenga siempre todos los archivos de registro separados hasta que la base de datos se haya adjuntado correctamente sin ellos.  
  
    > [!NOTE]  
    >  Si intenta adjuntar la base de datos sin especificar el archivo de registro, la operación de adjuntar buscará el archivo de registro en su ubicación original. Si la copia original del registro todavía está en esa ubicación, se adjuntará esa copia. Para evitar que se utilice el archivo de registro original, especifique la ruta de acceso del nuevo archivo de registro o elimine la copia original del archivo de registro (después de copiarlo en la nueva ubicación).  
  
3.  Adjunte los archivos copiados a la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, consulte [Attach a Database](../../relational-databases/databases/attach-a-database.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente actualiza una copia de una base de datos de una versión anterior de SQL Server. Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecutan en una ventana del Editor de consultas que esté conectada a la instancia del servidor a la que se ha adjuntado.  
  
1.  Separe la base de datos ejecutando las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```sql  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  Mediante el método que elija, copie los archivos de datos y de registro a la nueva ubicación.  
  
    > [!IMPORTANT]  
    > En el caso de una base de datos de producción, se recomienda colocar la base de datos y el registro de transacciones en discos independientes. Controlan diferentes requisitos de E/S y crecimiento de archivos, y mantenerlos independientes se considera un procedimiento recomendado.  
  
    Para copiar archivos a través de la red en un disco de un equipo remoto, use el nombre UNC (Convención de nomenclatura universal) de la ubicación remota. Un nombre UNC tiene el formato `\\Servername\Sharename\Path\Filename`. De la misma forma que al escribir archivos en el disco duro local, se debe conceder a la cuenta de usuario que usa la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los permisos necesarios para leer o escribir en archivos del disco remoto.  
  
3.  Adjunte la base de datos movida y, opcionalmente, su registro ejecutando la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```sql  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
    En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], una base de datos recién adjuntada no es inmediatamente visible en el Explorador de objetos. Para ver la base de datos, en el Explorador de objetos, haga clic en **Ver** y, a continuación, en **Actualizar**. Cuando se expande el nodo **Bases de datos** en el Explorador de objetos, la base de datos recién adjuntada aparecerá en la lista de bases de datos.  
  
##  <a name="FollowUp"></a> Seguimiento: Después de actualizar una base de datos de SQL Server  
Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **upgrade_option** . Si la opción de actualización se establece en importar (**upgrade_option** = 2) o en volver a generar (**upgrade_option** = 0), los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Observe también que cuando la opción de actualización se establece en importar, se vuelven a generar los índices de texto completo asociados si no se dispone de un catálogo de texto completo. Para cambiar el valor de la propiedad de servidor **upgrade_option** , use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
### <a name="dbcompat"></a> Nivel de compatibilidad de la base de datos después de la actualización  
Si el nivel de compatibilidad de una base de datos de usuario es 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad es 90 antes de la actualización en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>Administrar metadatos en la instancia de servidor actualizada  
Al adjuntar una base de datos a otra instancia de servidor, para que los usuarios y las aplicaciones puedan utilizarla de igual manera, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos, como los inicios de sesión, los trabajos y los permisos, en la otra instancia de servidor. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>La clave maestra de servicio y el cifrado de la clave maestra de la base de datos cambia de 3DES a AES  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores usan el algoritmo de cifrado AES para proteger la clave maestra de servicio (SMK) y la clave maestra de la base de datos (DMK). AES es un algoritmo de cifrado más reciente que el algoritmo 3DES empleado en versiones anteriores. La primera vez que se adjunta una base de datos o se restaura en una instancia nueva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aún no se ha almacenado una copia de la clave maestra de la base de datos (cifrada por la clave maestra de servicio) en el servidor. Debe usar la instrucción `OPEN MASTER KEY` para descifrar la clave maestra de la base de datos (DMK). Una vez que se ha descifrado la clave maestra de la base de datos, tiene la posibilidad de habilitar el descifrado automático en el futuro usando la instrucción `ALTER MASTER KEY REGENERATE` para proporcionar al servidor una copia de la clave maestra de la base de datos cifrada con la clave maestra de servicio (SMK). Cuando una base de datos se haya actualizado desde una versión anterior, se debe volver a generar la DMK para usar el algoritmo AES más reciente. Para obtener más información sobre cómo volver a generar la DMK, vea [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). El tiempo necesario para volver a generar la DMK con el fin de actualizarse a AES depende del número de objetos protegidos por la DMK. Solo es necesario volver a generar la DMK una vez y no tiene ningún efecto sobre las nuevas generaciones futuras como parte de una estrategia de rotación de claves.  
  
  
