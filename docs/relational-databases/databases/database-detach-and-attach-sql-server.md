---
title: Anexión y separación de bases de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b6ee22299c854193d15e5fe4d1e2daabf7250bb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68037585"
---
# <a name="database-detach-and-attach-sql-server"></a>Adjuntar y separar bases de datos (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Los archivos de registro de datos y transacciones de una base de datos se pueden desasociar y volverse a adjuntar posteriormente a la misma instancia u otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Separar y adjuntar una base de datos es útil si desea cambiar la base de datos a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo o si desea mover la base de datos.  
  
  
##  <a name="Security"></a> Seguridad  
Los permisos de acceso a archivos se establecen durante una serie de operaciones de base de datos, incluidas las operaciones de desasociar o adjuntar una base de datos.  
  
> [!IMPORTANT]  
> Se recomienda no adjuntar ni restaurar bases de datos de orígenes desconocidos o que no sean de confianza. Es posible que dichas bases de datos contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física.   
> Para usar una base de datos desde un origen desconocido o que no sea de confianza, ejecute [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) en la base de datos de un servidor que no sea de producción y examine también el código, como procedimientos almacenados u otro código definido por el usuario, en la base de datos.  
  
##  <a name="DetachDb"></a> Separar una base de datos  
Al separar una base de datos, la está quitando de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero la deja intacta en sus archivos de datos y en los archivos de registro de transacciones. Estos archivos pueden utilizarse después para adjuntar la base de datos a cualquier instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluido el servidor del que se separó.  
  
No podrá separar una base de datos si se cumple cualquiera de las condiciones siguientes:  
  
-   La base de datos está replicada y publicada. Si está replicada, la base de datos no debe estar publicada. Antes de separarla, debe deshabilitar la publicación ejecutando [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
  
    > [!NOTE]  
    > Si no puede usar **sp_replicationdboption**, puede quitar la replicación ejecutando [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md).  
  
-   Existe una instantánea de base de datos en la base de datos.  
  
    Para poder separar la base de datos, debe quitar todas sus instantáneas. Para obtener más información, vea [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
    > [!NOTE]  
    > No puede separar ni adjuntar una instantánea de base de datos.  
  
-   Se va a reflejar la base de datos en una sesión de creación de reflejo de la base de datos.  
  
    No se puede separar la base de datos a menos que se termine la sesión. Para obtener más información, vea [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
-   La base de datos es sospechosa. Una base de datos sospechosa no puede ser separada. Antes de poder separarla, debe ponerla en modo de emergencia. Para obtener más información sobre cómo poner una base de datos en modo de emergencia, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-  La base de datos es una base de datos del sistema.  
  
### <a name="backup-and-restore-and-detach"></a>Hacer copias de seguridad y restauración, y separar  
Al separar una base de datos de solo lectura se pierde información acerca de las bases diferenciales de las copias de seguridad diferenciales. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
### <a name="responding-to-detach-errors"></a>Responder a errores de separación  
Los errores generados durante la separación de una base de datos pueden impedir que la base de datos se cierre sin problemas y que se vuelva a generar el registro de transacciones. Si recibe un mensaje de error, realice las siguientes acciones correctoras:  
  
1.  Vuelva a adjuntar todos los archivos asociados a la base de datos, no solo el archivo principal.  
  
2.  Resuelva el problema que causó el mensaje de error.  
  
3.  Vuelva a separar la base de datos.  
  
##  <a name="AttachDb"></a> Adjuntar una base de datos  
Puede adjuntar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copiada o separada. Al adjuntar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que contiene los archivos de catálogo de texto completo a una instancia del servidor de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , los archivos de catálogo se adjuntan de su ubicación anterior junto con los demás archivos de base de datos, igual que en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obtener más información, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
Al adjuntar una base de datos, todos los archivos de datos deben estar disponibles (archivos MDF y NDF). Si algún archivo de datos tiene una ruta de acceso diferente a la que tenía cuando se creó la base de datos o cuando ésta se adjuntó por última vez, debe especificar la ruta actual.  
  
> [!NOTE]  
> Si el archivo de datos principal que se va a adjuntar es de solo lectura, [!INCLUDE[ssDE](../../includes/ssde-md.md)] considera que la base de datos es de solo lectura.  
  
Cuando se adjunta una base de datos cifrada a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por primera vez, el propietario debe abrir la clave maestra de esa base de datos mediante la ejecución de la instrucción siguiente: `OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'`. Se recomienda habilitar el descifrado automático de la clave maestra mediante la ejecución de la instrucción siguiente: `ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY`. Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) y [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md).  
  
 Las condiciones para adjuntar archivos de registro dependen, en parte, de si la base de datos es de lectura y escritura o de solo lectura. Vea a continuación:  
  
-   Para una base de datos de lectura y escritura, normalmente, podrá adjuntar un archivo de registro a una ubicación nueva. Sin embargo, en algunos casos, para volver a adjuntar una base de datos son necesarios sus archivos de registro. Por tanto, es importante mantener siempre todos los archivos de registro separados hasta que la base de datos se haya adjuntado correctamente sin ellos.  
  
    Si una base de datos de lectura y escritura contiene solo un archivo de registro y no se especifica una ubicación nueva para el mismo, al adjuntar la base de datos se buscará el archivo en la ubicación antigua. Si se encuentra, se usará el archivo de registro antiguo, sin tener en cuenta si la base de datos se cerró correctamente. No obstante, si el archivo de registro antiguo no se encuentra, la base de datos se cerró correctamente y no hay ninguna cadena de registros activa, al adjuntar se intentará crear un archivo de registro nuevo para la base de datos.  
  
-   Si el archivo de datos principal que se va a adjuntar es de solo lectura, [!INCLUDE[ssDE](../../includes/ssde-md.md)] considera que la base de datos es de solo lectura. Para una base de datos de solo lectura, los archivos de registro deben estar disponibles en la ubicación especificada en el archivo principal de la base de datos. No se puede compilar un archivo de registro nuevo porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede actualizar la ubicación del registro almacenada en el archivo principal.  
 
###  <a name="Metadata"></a> Cambios en los metadatos al adjuntar una base de datos  
Cuando se separa y se vuelve a adjuntar una base de datos de solo lectura, se pierde la información de copia de seguridad acerca de la base diferencial. La *base diferencial* es la copia de seguridad más reciente de todos los datos de una base de datos o de un subconjunto de archivos o grupos de archivos de la misma. Sin la información de la copia de seguridad básica, la base de datos **maestra** deja de estar sincronizada con la base de datos de solo lectura, de modo que las copias de seguridad diferenciales tomadas después pueden proporcionar resultados inesperados. Por lo tanto, si utiliza copias de seguridad diferenciales con una base de datos de solo lectura, deberá establecer una nueva base diferencial actual realizando una copia de seguridad completa después de volver a adjuntar la base de datos. Para obtener más información sobre las copias de seguridad diferenciales, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
Al adjuntar, la base de datos se inicia. Normalmente, al adjuntar una base de datos, esta vuelve al mismo estado en el que estaba cuando fue separada o copiada. Sin embargo, las operaciones de adjuntar y separar deshabilitan el encadenamiento de propiedades entre bases de datos para la base de datos. Para obtener más información sobre cómo habilitar el encadenamiento, vea [cross db ownership chaining (opción de configuración del servidor)](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md). 

 > [!IMPORTANT]
 > De forma predeterminada y por motivos de seguridad, las opciones de *is_broker_enabled*, *is_honor_broker_priority_on* e *is_trustworthy_on* se establecen en OFF siempre que se adjunta la base de datos. Para información sobre cómo activar estas opciones, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  Para más información sobre los metadatos, vea [Administración de los metadatos cuando una base de datos pasa a estar disponible en otro servidor](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).
  
### <a name="backup-and-restore-and-attach"></a>Hacer copias de seguridad y restauración, y adjuntar  
Al igual que cualquier base de datos que esté total o parcialmente sin conexión, no es posible adjuntar una base de datos con archivos que se estén restaurando. Puede adjuntar la base de datos si detiene la secuencia de restauración. Posteriormente, puede reiniciar la secuencia de restauración.  
  
###  <a name="OtherServerInstance"></a> Adjuntar una base de datos a otra instancia de servidor  
  
> [!IMPORTANT]  
> Una base de datos creada por una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede adjuntarse en versiones anteriores. Esto evita que la base de datos se use físicamente con una versión anterior de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. Pero esto se relaciona con el estado de los metadatos y no afecta al [nivel de compatibilidad de la base de datos](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md). Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).   
  
Al adjuntar una base de datos a otra instancia de servidor, es posible que tenga que volver a crear una parte o la totalidad de los metadatos de la base de datos, por ejemplo los inicios de sesión y los trabajos, en la otra instancia de servidor; de este modo se proporciona una experiencia coherente a usuarios y aplicaciones. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
**Para separar una base de datos**  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [Separar una base de datos](../../relational-databases/databases/detach-a-database.md)  
  
**Para adjuntar una base de datos**  
  
-   [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [Adjuntar una base de datos](../../relational-databases/databases/attach-a-database.md)  
  
-   [sp_attach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md)  
  
-   [sp_attach_single_file_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md)  
  
**Para actualizar una base de datos mediante el método de separar y adjuntar**  
  
-   [Actualizar una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
**Para mover una base de datos mediante el método de separar y adjuntar**  
  
-   [Mover una base de datos mediante Separar y Adjuntar &#40;Transact-SQL&#41;](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)  
  
**Para eliminar una instantánea de base de datos**  
  
-   [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
