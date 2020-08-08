---
title: Conexión a Azure SQL Database (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8e288b91c92d8d086d5b066f95868fa0fa733bb9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935964"
---
# <a name="connecting-to-azure-sql-database-mysqltosql"></a>Conexión a Azure SQL Database (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Azure, debe conectarse a la instancia de destino de SQL Azure. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de SQL Azure y muestra los metadatos de la base de datos en el explorador de metadatos de SQL Azure. SSMA almacena información de la instancia de SQL Azure a la que está conectado, pero no almacena contraseñas.  
  
La conexión a SQL Azure permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en SQL Azure y migre los datos.  
  
Los metadatos sobre la instancia de SQL Azure no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en SQL Azure explorador de metadatos, debe actualizar manualmente los metadatos de SQL Azure. Para obtener más información, vea la sección "sincronizar metadatos de SQL Azure" más adelante en este tema.  
  
## <a name="required-sql-azure-permissions"></a>Permisos SQL Azure necesarios  
La cuenta que se usa para conectarse a SQL Azure requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
-   Para convertir objetos MySQL en [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, actualizar metadatos de SQL Azure o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Azure.  
  
-   Para cargar los objetos de base de datos en SQL Azure, el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Establecer una conexión SQL Azure  
Antes de convertir los objetos de base de datos de MySQL en SQL Azure sintaxis, debe establecer una conexión con la instancia de SQL Azure en la que desea migrar la base de datos o las bases de datos de MySQL.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de MySQL después de conectarse a SQL Azure. Para obtener más información, consulte [asignación de bases de datos de MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Azure, asegúrese de que la instancia de SQL Azure se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Azure**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Azure** (esta opción se habilita después de la creación de un proyecto).  
  
    Si previamente se ha conectado a SQL Azure, el nombre del comando se volverá **a conectar a SQL Azure**.  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre del servidor de SQL Azure.  
  
3.  Escriba, seleccione o **examine** el nombre de la base de datos.  
  
4.  Escriba o seleccione el **nombre de usuario**.  
  
5.  Escriba la **contraseña**.  
  
6.  SSMA recomienda una conexión cifrada para SQL Azure.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para MySQL no admite la conexión a la base de datos **maestra** en SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizar metadatos de SQL Azure  
Los metadatos acerca de las bases de datos de Azure SQL Database no se actualizan automáticamente. Los metadatos de SQL Azure explorador de metadatos es una instantánea de los metadatos cuando se conectó por primera vez a SQL Azure, o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Azure.  
  
2.  En SQL Azure explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a bases de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre los esquemas de MySQL y Azure SQL Database, consulte [asignación de bases de datos de MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar las opciones de configuración de los proyectos, vea [establecer opciones de proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de SQL Server y MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de MySQL en SQL Azure definiciones de objeto. Para obtener más información, vea [convertir las bases de datos MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de MySQL a SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
