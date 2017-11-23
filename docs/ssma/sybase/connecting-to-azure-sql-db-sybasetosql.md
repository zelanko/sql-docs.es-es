---
title: Conectarse a la base de datos de SQL Azure (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31c5fe416166627ac63f0f65e3b8c1102fc48f8e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conectarse a la base de datos de SQL Azure (SybaseToSQL)
Para migrar las bases de datos de Sybase a base de datos de SQL Azure, debe conectarse a la instancia de destino de la base de datos de SQL Azure. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de base de datos de SQL Azure y muestra los metadatos de la base de datos en el Explorador de metadatos de base de datos de SQL Azure. SSMA almacena la información de la instancia de base de datos de SQL de Azure están conectados a, pero no almacena las contraseñas.  
  
La conexión a la base de datos de SQL Azure permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, deben volver a conectarse a la base de datos de SQL Azure si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en la base de datos de SQL Azure y migrar los datos.  
  
Metadatos acerca de la instancia de base de datos de SQL Azure no se sincronizarán automáticamente. En su lugar, para actualizar los metadatos en el Explorador de metadatos de base de datos de SQL Azure, debe actualizar manualmente los metadatos de la base de datos de SQL Azure. Para obtener más información, vea la sección "Sincronización de metadatos de base de datos de SQL de Azure" más adelante en este tema.  
  
## <a name="required-azure-sql-db-permissions"></a>Requiere permisos de base de datos de SQL Azure  
La cuenta que se usa para conectarse a la base de datos de SQL Azure requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
1.  Para convertir objetos de Sybase a [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, para actualizar los metadatos de la base de datos de SQL Azure, o para guardar la sintaxis para convertir las secuencias de comandos, la cuenta debe tener permiso para iniciar sesión en la instancia de base de datos de SQL Azure.  
  
2.  Para cargar objetos de base de datos en la base de datos de SQL Azure, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Establecer una conexión de base de datos de SQL Azure  
Para convertir objetos de base de datos de Sybase a la sintaxis de la base de datos de SQL Azure, debe establecer una conexión a la instancia de base de datos de SQL de Azure donde van a migrar la base de datos de Sybase o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos que se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de Sybase después de conectarse a la base de datos de SQL Azure. Para obtener más información, vea [asignación Sybase ASE esquemas para esquemas de SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de intentar conectarse a la base de datos de SQL Azure, asegúrese de que la instancia de base de datos de SQL Azure se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a la base de datos de SQL Azure**  
  
1.  En el **archivo** menú, seleccione **conectar con base de datos de SQL Azure**(esta opción se habilita después de la creación de un proyecto).  
  
    Si se ha conectado anteriormente a la base de datos de SQL Azure, el nombre de comando será **conectarse de nuevo a la base de datos de SQL Azure**  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre del servidor de base de datos de SQL Azure.  
  
3.  Escriba, seleccione o **examinar** el nombre de la base de datos.  
  
4.  Escriba o seleccione **nombre de usuario**.  
  
5.  Escriba el **contraseña**.  
  
6.  SSMA recomienda conexión cifrada a la base de datos de SQL Azure.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite la conexión a **maestro** base de datos en la base de datos de SQL Azure.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronizar los metadatos de base de datos de SQL Azure  
Metadatos acerca de las bases de datos de la base de datos de SQL Azure no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de base de datos de SQL Azure están una instantánea de los metadatos cuando conectó por primera vez a la base de datos de SQL Azure, o la última vez que actualizar manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos u objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a la base de datos de SQL Azure.  
  
2.  En el Explorador de metadatos de base de datos de SQL Azure, active la casilla de verificación junto a la base de datos o el esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con la base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de Sybase y los esquemas y las bases de datos de la base de datos de SQL Azure, vea [esquemas de asignación Sybase ASE para esquemas de SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [establecer las opciones del proyecto &#40; SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Si no tiene que realizar cualquiera de estas tareas, puede convertir las definiciones de objeto de base de datos de Sybase a definiciones de objeto de base de datos de SQL Azure. Para obtener más información, vea [convertir objetos de base de datos de Sybase ASE &#40; SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
