---
title: Conectarse a Azure SQL DB (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ac8b97e36338a280b6f78a0e6bb73eeab882655d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632103"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conexión a Azure SQL DB (SybaseToSQL)
Para migrar las bases de datos de Sybase a Azure SQL DB, debe conectarse a la instancia de destino de la base de datos de SQL Azure. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de Azure SQL DB y muestra los metadatos de la base de datos en el Explorador de metadatos de base de datos de SQL Azure. SSMA almacena la información de la instancia de Azure SQL DB están conectados a, pero no almacena las contraseñas.  
  
La conexión a Azure SQL DB permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a Azure SQL DB si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en Azure SQL DB y migrar los datos.  
  
Metadatos acerca de la instancia de Azure SQL DB no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en el Explorador de metadatos de Azure SQL DB, debe actualizar manualmente los metadatos de la base de datos de SQL Azure. Para obtener más información, consulte la sección "Sincronización de Azure SQL DB Metadata" más adelante en este tema.  
  
## <a name="required-azure-sql-db-permissions"></a>Requiere permisos de base de datos de SQL Azure  
La cuenta que se usa para conectarse a Azure SQL DB requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
1.  Para convertir objetos de Sybase a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, para actualizar los metadatos de la base de datos de SQL Azure, o para guardar la sintaxis para convertir los scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de base de datos de SQL Azure.  
  
2.  Para cargar los objetos de base de datos en Azure SQL DB, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Establecer una conexión de base de datos de SQL Azure  
Antes de convertir los objetos de base de datos de Sybase a la sintaxis de la base de datos de SQL Azure, debe establecer una conexión a la instancia de Azure SQL DB donde van a migrar la base de datos de Sybase o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos donde se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de Sybase después de conectarse a Azure SQL DB. Para obtener más información, consulte [asignación de esquemas de Sybase ASE a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de intentar conectarse a Azure SQL DB, asegúrese de la instancia de Azure SQL DB se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a Azure SQL DB**  
  
1.  En el **archivo** menú, seleccione **Connect a Azure SQL DB**(esta opción está habilitada después de la creación de un proyecto).  
  
    Si se ha conectado anteriormente a Azure SQL DB, será el nombre del comando **volver a conectar a Azure SQL DB**  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre del servidor de base de datos de SQL Azure.  
  
3.  Escriba, seleccione o **examinar** el nombre de la base de datos.  
  
4.  Escriba o seleccione **UserName**.  
  
5.  Escriba el **contraseña**.  
  
6.  SSMA recomienda conexión cifrada a Azure SQL DB.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite conexiones a **maestro** base de datos en Azure SQL DB.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronizar los metadatos de base de datos de SQL Azure  
Metadatos acerca de las bases de datos de Azure SQL DB no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de Azure SQL DB están una instantánea de los metadatos cuando se conectó en primer lugar a la base de datos de SQL Azure o la última vez que actualizar manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos única o un objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a Azure SQL DB.  
  
2.  En el Explorador de metadatos de Azure SQL DB, seleccione la casilla de verificación junto a la base de datos o esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de Sybase y bases de datos de SQL Azure y esquemas, vea [esquemas de asignación de Sybase ASE a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [definir opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Si no es necesario realizar ninguna de estas tareas, puede convertir las definiciones de objeto de base de datos de Sybase en definiciones de objetos de base de datos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
