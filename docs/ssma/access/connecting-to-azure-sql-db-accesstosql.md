---
title: Conectarse a Azure SQL DB (AccessToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8924ffbbbbbedccdc3bb99469c92667efb822a4c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138933"
---
# <a name="connecting-to-azure-sql-db-accesstosql"></a>Conectarse a Azure SQL DB (AccessToSQL)
Para migrar las bases de datos de Access a SQL Azure, debe conectarse a la instancia de destino de SQL Azure. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de SQL Azure y muestra los metadatos de la base de datos en el Explorador de metadatos de SQL Azure. SSMA almacena información acerca de qué instancia de SQL Azure está conectado a, pero no almacena las contraseñas.  
  
La conexión a SQL Azure permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Azure y migrar los datos.  
  
No se sincronizan automáticamente los metadatos sobre la instancia de SQL Azure. En su lugar, para actualizar los metadatos en el Explorador de metadatos de SQL Azure, debe actualizar manualmente los metadatos de SQL Azure. Para obtener más información, consulte la sección "Sincronización de metadatos de SQL Azure" más adelante en este tema.  
  
## <a name="required-sql-azure-permissions"></a>Requiere SQL Azure permisos  
La cuenta que se usa para conectarse a SQL Azure requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, para actualizar los metadatos de SQL Azure, o para guardar la sintaxis para convertir los scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Azure.  
  
-   Para cargar los objetos de base de datos en SQL Azure, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Establecer un SQL Azure la conexión  
Antes de convertir los objetos de base de datos de acceso a la sintaxis de SQL Azure, debe establecer una conexión a la instancia de SQL Azure donde van a migrar la base de datos o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos donde se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de acceso después de conectarse a SQL Azure. Para obtener más información, consulte [asignación de bases de datos de Access a esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md)  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Azure, asegúrese de que la instancia de SQL Azure se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Azure**  
  
1.  En el **archivo** menú, seleccione **conectarse a SQL Azure** (esta opción está habilitada después de la creación de un proyecto).  
  
    Si se ha conectado anteriormente a SQL Azure, será el nombre del comando **volver a conectar a SQL Azure**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre del servidor de SQL Azure.  
  
3.  Escriba, seleccione o **examinar** el nombre de la base de datos.  
  
4.  Escriba o seleccione **UserName**.  
  
5.  Escriba el **contraseña**.  
  
6.  SSMA recomienda conexión cifrada a SQL Azure.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Access no admite conexiones a **maestro** base de datos en SQL Azure.  
  
Si no hay ninguna base de datos en la cuenta de SQL Azure, puede crear la primera base de datos mediante **crear base de datos de Azure** opciones que aparece al hacer clic en **examinar** botón.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronización de SQL Azure metadatos  
Metadatos acerca de las bases de datos de SQL Azure no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de SQL Azure están una instantánea de los metadatos cuando conectó en primer lugar a SQL Azure o la última vez que usted manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos única o un objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Azure.  
  
2.  En el Explorador de metadatos de SQL Azure, active la casilla de verificación junto a la base de datos o esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con base de datos**.  
  
## <a name="refreshing-sql-azure-metadata"></a>Actualización de SQL Azure metadatos  
Si los esquemas de SQL Azure cambian después de conectarse, puede actualizar los metadatos del servidor.  
  
**Para actualizar los metadatos de SQL Azure**  
  
-   Haga clic en el Explorador de metadatos de SQL Azure, **bases de datos**y, a continuación, seleccione **actualizar desde la base de datos**.  
  
## <a name="reconnecting-to-sql-azure"></a>Volver a conectarse a SQL Azure  
La conexión a SQL Azure permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Azure y migrar los datos.  
  
El procedimiento para volver a conectarse a SQL Azure es el mismo que el procedimiento para establecer una conexión.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de acceso y los esquemas y las bases de datos de SQL Azure, consulte [bases de datos de asignación de acceso a los esquemas de SQL Server](mapping-source-and-target-databases-accesstosql.md).  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [definir opciones de proyecto](setting-conversion-and-migration-options-accesstosql.md).  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [tipos de datos de destino y origen de asignación](mapping-source-and-target-data-types-accesstosql.md).  
  
-   Si no es necesario realizar ninguna de estas tareas, puede convertir las definiciones de objeto de base de datos de acceso en las definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir bases de datos de Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
