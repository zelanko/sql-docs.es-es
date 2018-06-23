---
title: Base de datos maestra (master) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], about
- master database [SQL Server]
ms.assetid: 660e909f-61eb-406b-bbce-8864dd629ba0
caps.latest.revision: 46
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 88cbd58a75ff8b7ceaaf93843bb685cdcb8dc11b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197412"
---
# <a name="master-database"></a>Base de datos maestra
  La base de datos **maestra** registra toda la información de sistema de un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Dentro de esta información se incluyen los metadatos de una sola instancia, como las cuentas de inicio de sesión, los extremos, los servidores vinculados y la configuración del sistema. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los objetos de sistema ya no se almacenan en la base de datos **maestra** , sino en la [base de datos de recursos](resource-database.md). Asimismo, **maestra** es la base de datos que registra la existencia de las demás bases de datos, la ubicación de los archivos de las bases de datos y la información de inicialización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede iniciarse si la base de datos **maestra** no está disponible.  
  
## <a name="physical-properties-of-master"></a>Propiedades físicas de la base de datos maestra  
 En la siguiente tabla se enumeran los valores de configuración iniciales de los archivos de registro y datos **maestros** . El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Crecimiento del archivo|  
|----------|------------------|-------------------|-----------------|  
|Datos principales|maestra|master.mdf|Crecimiento automático del 10 por ciento hasta llenar el disco.|  
|Log|mastlog|mastlog.ldf|Crecimiento automático del 10 por ciento hasta un máximo de 2 terabytes.|  
  
 Para obtener información sobre cómo mover los archivos de registro y los datos **maestros** , vea [Mover bases de datos del sistema](system-databases.md).  
  
### <a name="database-options"></a>Opciones de base de datos  
 En la siguiente tabla se enumera el valor predeterminado de cada opción de base de datos en la base de datos **maestra** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
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
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|Sí|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|DISABLE_BROKER|no|  
|TRUSTWORTHY|OFF|Sí|  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrictions  
 Las siguientes operaciones no se pueden realizar en la base de datos **maestra** :  
  
-   Agregar archivos o grupos de archivos.  
  
-   Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
  
-   Cambiar el propietario de la base de datos. **master** es propiedad de **sa**.  
  
-   Crear un catálogo de texto completo o un índice de texto completo.  
  
-   Crear desencadenadores en las tablas del sistema de la base de datos.  
  
-   Eliminar la base de datos.  
  
-   Eliminar el usuario **guest** de la base de datos.  
  
-   Habilitar el mecanismo de captura de cambios en los datos.  
  
-   Participar en el reflejo de la base de datos.  
  
-   Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
  
-   Cambiar el nombre de la base de datos o del grupo de archivos principal.  
  
-   Establecer la base de datos en OFFLINE.  
  
-   Establecer la base de datos o el grupo de archivos principal en READ_ONLY.  
  
## <a name="recommendations"></a>Recomendaciones  
 Cuando trabaje con la base de datos **maestra** , tenga en cuenta las siguientes recomendaciones:  
  
-   Tenga siempre disponible una copia de seguridad actualizada de la base de datos **maestra** .  
  
-   Haga una copia de seguridad de la base de datos **maestra** lo antes posible después de realizar las siguientes operaciones:  
  
    -   Crear, modificar o eliminar una base de datos  
  
    -   Cambiar los valores de configuración del servidor o de la base de datos  
  
    -   Modificar o agregar las cuentas de inicio de sesión  
  
-   No cree objetos de usuario en **maestra**. Si lo hace, deberá realizar una copia de seguridad de la base de datos **maestra** con más frecuencia.  
  
-   No establezca la opción TRUSTWORTHY en ON para la base de datos **maestra** .  
  
## <a name="what-to-do-if-master-becomes-unusable"></a>Qué hacer si la base de datos maestra queda inutilizable  
 Si la base de datos **maestra** está inutilizable, puede devolverla a un estado válido de dos formas:  
  
-   Restaure la base de datos **maestra** desde una copia de seguridad de la base de datos actual.  
  
     Si puede iniciar la instancia de servidor, debería poder restaurar la base de datos **maestra** desde una copia de seguridad completa de la base de datos. Para obtener más información, vea [Restaurar la base de datos maestra &#40;Transact-SQL&#41;](../backup-restore/restore-the-master-database-transact-sql.md).  
  
-   Vuelva a generar la base de datos **maestra** completamente.  
  
     Si no puede iniciar **a causa de daños graves en la base de datos** maestra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deberá volver a generar la base de datos **maestra**. Para obtener más información, vea [Volver a generar bases de datos del sistema](rebuild-system-databases.md).  
  
    > [!IMPORTANT]  
    >  Al recompilar la base de datos **maestra** , se recompilan todas las bases de datos del sistema.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Volver a generar bases de datos del sistema](rebuild-system-databases.md)  
  
 [Bases de datos del sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover archivos de base de datos](move-database-files.md)  
  
  
