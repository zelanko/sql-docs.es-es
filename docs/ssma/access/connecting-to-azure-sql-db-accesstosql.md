---
title: Conexión a Azure SQL DB (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instance of SQL Azure
- metadata, refreshing
- refreshing metadata
- SQL Azure
- SQL Azure, connecting
- SQL Azure, connecting to
- SQL Azure, reconnecting
- SQL Azure, synchronizing metadata
ms.assetid: 1ba0d113-dc05-4431-8689-e14a8821bafd
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6c35168f1c77f0574b202b77da515dab497a3ec7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006657"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Conexión a Azure SQL DB (AccessToSQL)
Para migrar bases de datos de Access a SQL Azure, debe conectarse a la instancia de destino de SQL Azure. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de SQL Azure y muestra los metadatos de la base de datos en el explorador de metadatos de SQL Azure. SSMA almacena información acerca de la instancia de SQL Azure a la que está conectado, pero no almacena contraseñas.  
  
La conexión a SQL Azure permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en SQL Azure y migre los datos.  
  
Los metadatos sobre la instancia de SQL Azure no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en SQL Azure explorador de metadatos, debe actualizar manualmente los metadatos de SQL Azure. Para obtener más información, vea la sección "sincronizar metadatos de SQL Azure" más adelante en este tema.  
  
## <a name="required-sql-azure-permissions"></a>Permisos SQL Azure necesarios  
La cuenta que se usa para conectarse a SQL Azure requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de Access [!INCLUDE[tsql](../../includes/tsql-md.md)] en sintaxis, actualizar metadatos de SQL Azure o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Azure.  
  
-   Para cargar los objetos de base de datos en SQL Azure, el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Establecer una conexión SQL Azure  
Antes de convertir los objetos de base de datos de Access en SQL Azure sintaxis, debe establecer una conexión con la instancia de SQL Azure en la que desea migrar la base de datos o las bases de datos de Access.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de acceso después de conectarse a SQL Azure. Para obtener más información, consulte [asignación de bases de datos de Access a esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md) .  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Azure, asegúrese de que la instancia de SQL Azure se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Azure**  
  
1.  En el menú **archivo** , seleccione **conectarse a SQL Azure** (esta opción se habilita después de la creación de un proyecto).  
  
    Si anteriormente se conectó a SQL Azure, el nombre del comando se volverá **a conectar a SQL Azure**.  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre del servidor de SQL Azure.  
  
3.  Escriba, seleccione o **examine** el nombre de la base de datos.  
  
4.  Escriba o seleccione el **nombre de usuario**.  
  
5.  Escriba la **contraseña**.  
  
6.  SSMA recomienda una conexión cifrada para SQL Azure.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Access no admite la conexión a la base de datos **maestra** en SQL Azure.  
  
Si no hay ninguna base de datos en la cuenta de SQL Azure, puede crear la primera base de datos mediante la opción **crear base de datos de Azure** que aparece en el botón hacer clic en **examinar** .  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizar metadatos de SQL Azure  
Los metadatos acerca de SQL Azure bases de datos no se actualizan automáticamente. Los metadatos de SQL Azure explorador de metadatos es una instantánea de los metadatos cuando se conectó por primera vez a SQL Azure, o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Azure.  
  
2.  En SQL Azure explorador de metadatos, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a bases de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Actualización de metadatos de SQL Azure  
Si SQL Azure esquemas cambian después de conectarse, puede actualizar los metadatos desde el servidor.  
  
**Para actualizar SQL Azure metadatos**  
  
-   En SQL Azure explorador de metadatos, haga clic con el botón derecho en **bases**de datos y seleccione **actualizar desde base de**datos.  
  
## <a name="reconnecting-to-sql-azure"></a>Volver a conectar a SQL Azure  
La conexión a SQL Azure permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en SQL Azure y migre los datos.  
  
El procedimiento para volver a conectar a SQL Azure es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de acceso y bases de datos y esquemas de SQL Azure, consulte [asignación de bases de datos de Access a esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md).  
  
-   Para personalizar las opciones de configuración de los proyectos, consulte [configuración de las opciones del proyecto](setting-conversion-and-migration-options-accesstosql.md).  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, vea [asignar tipos de datos de origen y de destino](mapping-source-and-target-data-types-accesstosql.md).  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de Access en SQL Azure definiciones de objeto. Para obtener más información, vea [convertir bases](converting-access-database-objects-accesstosql.md) de datos de Access.  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
