---
title: Conectarse a Azure SQL DB (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 63d3bb997d7ad9fc32d541202bf07ab66676259d
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2018
ms.locfileid: "40392355"
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Conexión a Azure SQL DB (MySQLToSQL)
Para migrar bases de datos MySQL a SQL Azure, debe conectarse a la instancia de destino de SQL Azure. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de SQL Azure y muestra los metadatos de la base de datos en el Explorador de metadatos de SQL Azure. SSMA almacena la información de la instancia de SQL Azure está conectado a, pero no almacena las contraseñas.  
  
La conexión a SQL Azure permanece activa hasta que cierre el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Azure y migrar los datos.  
  
No se sincronizan automáticamente los metadatos sobre la instancia de SQL Azure. En su lugar, para actualizar los metadatos en el Explorador de metadatos de SQL Azure, debe actualizar manualmente los metadatos de SQL Azure. Para obtener más información, consulte la sección "Sincronización de metadatos de SQL Azure" más adelante en este tema.  
  
## <a name="required-sql-azure-permissions"></a>Requiere SQL Azure permisos  
La cuenta que se usa para conectarse a SQL Azure requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de MySQL a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, para actualizar los metadatos de SQL Azure, o para guardar la sintaxis para convertir los scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Azure.  
  
-   Para cargar los objetos de base de datos en SQL Azure, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Establecer un SQL Azure la conexión  
Antes de convertir los objetos de base de datos MySQL en sintaxis de SQL Azure, debe establecer una conexión a la instancia de SQL Azure donde van a migrar la base de datos MySQL o bases de datos.  
  
Al definir las propiedades de conexión, también se especifique la base de datos donde se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de MySQL después de conectarse a SQL Azure. Para obtener más información, consulte [asignación de bases de datos MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
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
> SSMA para MySQL no admite conexiones a **maestro** base de datos en SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronización de SQL Azure metadatos  
Metadatos acerca de las bases de datos de SQL Azure no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de SQL Azure están una instantánea de los metadatos cuando conectó en primer lugar a SQL Azure o la última vez que usted manualmente los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos única o un objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Azure.  
  
2.  En el Explorador de metadatos de SQL Azure, active la casilla de verificación junto a la base de datos o esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre esquemas de MySQL y los esquemas y las bases de datos de SQL Azure, consulte [bases de datos de asignación de MySQL a esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [definir opciones de proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Si no es necesario realizar ninguna de estas tareas, puede convertir las definiciones de objeto de base de datos MySQL en definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir las bases de datos de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
