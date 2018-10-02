---
title: Base de datos maestra (master) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dad70b3deaf6b9412314f8f212b52268ba77dd61
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618533"
---
# <a name="master-database"></a>Base de datos maestra
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La base de datos **maestra** registra toda la información de sistema de un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Dentro de esta información se incluyen los metadatos de una sola instancia, como las cuentas de inicio de sesión, los extremos, los servidores vinculados y la configuración del sistema. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los objetos de sistema ya no se almacenan en la base de datos **maestra** , sino en la [base de datos de recursos](../../relational-databases/databases/resource-database.md). Asimismo, **maestra** es la base de datos que registra la existencia de las demás bases de datos, la ubicación de los archivos de las bases de datos y la información de inicialización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede iniciarse si la base de datos **maestra** no está disponible.  

> [!IMPORTANT]
> En el caso del servidor lógico de Azure SQL Database, solo se aplican la base de datos maestra y la base de datos tempdb. Para familiarizarse con el concepto de servidor lógico y base de datos maestra lógica, consulte [¿Qué es un servidor lógico de Azure SQL?](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-logical-server) Para ver información sobre tempdb en el contexto de Azure SQL Database, vea [Base de datos tempdb en SQL Database](tempdb-database.md#tempdb-database-in-sql-database). En el caso de Instancia administrada de Azure SQL Database, se aplican todas las bases de datos del sistema. Para más información sobre Instancias administradas en Azure SQL Database, consulte [¿Qué es Instancia administrada de SQL Database?](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
  
## <a name="physical-properties-of-master"></a>Propiedades físicas de la base de datos maestra  
En la siguiente tabla se enumeran los valores de configuración iniciales de los archivos de registro y datos **maestros** para SQL Server e Instancia administrada de Azure SQL Database. El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Crecimiento del archivo|  
|----------|------------------|-------------------|-----------------|  
|Datos principales|maestra|master.mdf|Crecimiento automático del 10 por ciento hasta llenar el disco.|  
|Log|mastlog|mastlog.ldf|Crecimiento automático del 10 por ciento hasta un máximo de 2 terabytes.|  
  
Para obtener información sobre cómo mover los archivos de registro y los datos **maestros** , vea [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  

> [!IMPORTANT]
> En el caso del servidor lógico de Azure SQL Database, el usuario no tiene control sobre el tamaño de la base de datos **maestra**.
  
### <a name="database-options"></a>Opciones de base de datos  
En la siguiente tabla se enumera el valor predeterminado de cada opción de base de datos en la base de datos **maestra** para SQL e Instancia administrada de Azure SQL Database y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
> [!IMPORTANT]
> En el caso del servidor lógico de Azure SQL Database, el usuario no tiene control sobre estas opciones de base de datos.

|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|no|  
|ANSI_NULL_DEFAULT|OFF|Sí|  
|ANSI_NULLS|OFF|Sí|  
|ANSI_PADDING|OFF|Sí|  
|ANSI_WARNINGS|OFF|Sí|  
|ARITHABORT|OFF|Sí|  
|AUTO_CLOSE|OFF|no|  
|AUTO_CREATE_STATISTICS|ON|Sí|  
|AUTO_SHRINK|OFF|no|  
|AUTO_UPDATE_STATISTICS|ON|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sí|  
|CHANGE_TRACKING|OFF|no|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sí|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|no<br /><br /> no<br /><br /> no|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sí|  
|DB_CHAINING|ON|no|  
|ENCRYPTION|OFF|no|  
|MIXED_PAGE_ALLOCATION|ON|no|  
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|Sí|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|DISABLE_BROKER|no|  
|TRUSTWORTHY|OFF|Sí|  
  
Para obtener una descripción de estas opciones de la base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="restrictions"></a>Restrictions  
Las siguientes operaciones no se pueden realizar en la base de datos **maestra** :  
  
- Agregar archivos o grupos de archivos.  
- Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
- Cambiar el propietario de la base de datos. **master** es propiedad de **sa**.  
- Crear un catálogo de texto completo o un índice de texto completo.  
- Crear desencadenadores en las tablas del sistema de la base de datos.  
- Eliminar la base de datos.  
- Eliminar el usuario **guest** de la base de datos.  
- Habilitar el mecanismo de captura de cambios en los datos.  
- Participar en el reflejo de la base de datos.  
- Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
- Cambiar el nombre de la base de datos o del grupo de archivos principal.  
- Establecer la base de datos en OFFLINE.  
- Establecer la base de datos o el grupo de archivos principal en READ_ONLY.  
  
## <a name="recommendations"></a>Recomendaciones  
Cuando trabaje con la base de datos **maestra** , tenga en cuenta las siguientes recomendaciones:  
  
- Tenga siempre disponible una copia de seguridad actualizada de la base de datos **maestra** .  
- Haga una copia de seguridad de la base de datos **maestra** lo antes posible después de realizar las siguientes operaciones:  
  
  - Crear, modificar o eliminar una base de datos  
  - Cambiar los valores de configuración del servidor o de la base de datos  
  - Modificar o agregar las cuentas de inicio de sesión  
  
- No cree objetos de usuario en **maestra**. Si lo hace, deberá realizar una copia de seguridad de la base de datos **maestra** con más frecuencia.  
- No establezca la opción TRUSTWORTHY en ON para la base de datos **maestra** .  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>Qué hacer si la base de datos maestra queda inutilizable  
 Si la base de datos **maestra** está inutilizable, puede devolverla a un estado válido de dos formas:  
  
- Restaure la base de datos **maestra** desde una copia de seguridad de la base de datos actual.  
  
  Si puede iniciar la instancia de servidor, debería poder restaurar la base de datos **maestra** desde una copia de seguridad completa de la base de datos. Para obtener más información, vea [Restaurar la base de datos maestra &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md).  
  
- Vuelva a generar la base de datos **maestra** completamente.  
  
  Si no puede iniciar **a causa de daños graves en la base de datos** maestra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deberá volver a generar la base de datos **maestra**. Para obtener más información, vea [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md).  
  
  > [!IMPORTANT]  
  >  Al recompilar la base de datos **maestra** , se recompilan todas las bases de datos del sistema.  
  
## <a name="related-content"></a>Contenido relacionado  
- [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md)  
- [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
- [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)  
