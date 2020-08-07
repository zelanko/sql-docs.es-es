---
title: Conexión a Azure SQL Database (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a16ade8d212d3d197b858488dde05b439d8e989f
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864762"
---
# <a name="connecting-to-azure-sql-database-sybasetosql"></a>Conexión a Azure SQL Database (SybaseToSQL)
Para migrar bases de datos de Sybase a Azure SQL Database, debe conectarse a la instancia de destino de Azure SQL Database. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de Azure SQL Database y muestra los metadatos de la base de datos en el explorador de metadatos de Azure SQL Database. SSMA almacena información de la instancia de Azure SQL Database a la que está conectado, pero no almacena contraseñas.  
  
La conexión a Azure SQL Database permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a Azure SQL Database si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en Azure SQL Database y migre los datos.  
  
Los metadatos sobre la instancia de Azure SQL Database no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en Azure SQL Database explorador de metadatos, debe actualizar manualmente los metadatos de Azure SQL Database. Para obtener más información, vea la sección "sincronizar metadatos de Azure SQL Database" más adelante en este tema.  
  
## <a name="required-azure-sql-database-permissions"></a>Permisos Azure SQL Database necesarios  
La cuenta que se usa para conectarse a Azure SQL Database requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
1.  Para convertir objetos de Sybase en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos de Azure SQL Database, o para guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de Azure SQL Database.  
  
2.  Para cargar los objetos de base de datos en Azure SQL Database, el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-an-azure-sql-database-connection"></a>Establecimiento de una conexión Azure SQL Database  
Antes de convertir los objetos de base de datos de Sybase en Azure SQL Database sintaxis, debe establecer una conexión con la instancia de Azure SQL Database en la que desea migrar la base de datos o las bases de datos de Sybase.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de Sybase después de conectarse a Azure SQL Database. Para obtener más información, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de intentar conectarse a Azure SQL Database, asegúrese de que la instancia de Azure SQL Database se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a Azure SQL Database**  
  
1.  En el menú **archivo** , seleccione **conectarse a Azure SQL Database**(esta opción se habilita después de la creación de un proyecto).  
  
    Si previamente se ha conectado a Azure SQL Database, el nombre del comando se volverá **a conectar a Azure SQL Database**  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre del servidor de Azure SQL Database.  
  
3.  Escriba, seleccione o **examine** el nombre de la base de datos.  
  
4.  Escriba o seleccione el **nombre de usuario**.  
  
5.  Escriba la **contraseña**.  
  
6.  SSMA recomienda una conexión cifrada para Azure SQL Database.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite la conexión a la base de datos **maestra** en Azure SQL Database.  
  
## <a name="synchronizing-azure-sql-database-metadata"></a>Sincronizar metadatos de Azure SQL Database  
Los metadatos acerca de Azure SQL Database bases de datos no se actualizan automáticamente. Los metadatos de Azure SQL Database explorador de metadatos es una instantánea de los metadatos cuando se conectó por primera vez a Azure SQL Database, o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a Azure SQL Database.  
  
2.  En Azure SQL Database explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a bases de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de Sybase y bases de datos y esquemas de Azure SQL Database, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar las opciones de configuración de los proyectos, vea [establecer opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de Sybase ase y SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de Sybase en Azure SQL Database definiciones de objeto. Para obtener más información, consulte [conversión de objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de Sybase ASE a SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
