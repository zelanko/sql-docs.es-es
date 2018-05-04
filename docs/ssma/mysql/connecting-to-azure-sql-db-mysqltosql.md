---
title: Conectarse a la base de datos de SQL Azure (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
ms.openlocfilehash: bb49a6e0604fd3bd713857bab18cde30804b0f42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Conectarse a la base de datos de SQL Azure (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Azure, debe conectarse a la instancia de destino de SQL Azure. Cuando se conecta, SSMA obtiene metadatos acerca de todas las bases de datos en la instancia de SQL Azure y muestra los metadatos de la base de datos en el Explorador de metadatos de SQL Azure. SSMA almacena la información de la instancia de SQL Azure están conectados a, pero no almacena las contraseñas.  
  
La conexión a SQL Azure permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a SQL Azure si desea que una conexión activa con el servidor. Puede trabajar sin conexión hasta que se cargará los objetos de base de datos en SQL Azure y migrar los datos.  
  
Metadatos acerca de la instancia de SQL Azure no se sincronizarán automáticamente. En su lugar, para actualizar los metadatos en el Explorador de metadatos de SQL Azure, debe actualizar manualmente los metadatos de SQL Azure. Para obtener más información, vea la sección "Sincronizar los metadatos de SQL Azure" más adelante en este tema.  
  
## <a name="required-sql-azure-permissions"></a>Requiere SQL Azure permisos  
La cuenta que se usa para conectarse a SQL Azure requiere permisos diferentes dependiendo de las acciones que realiza la cuenta:  
  
-   Para convertir objetos de MySQL a [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, para actualizar los metadatos de SQL Azure, o para guardar la sintaxis para convertir las secuencias de comandos, la cuenta debe tener permiso para iniciar sesión en la instancia de SQL Azure.  
  
-   Para cargar objetos de base de datos en SQL Azure, el requisito de permiso mínimo es la pertenencia a la **db_owner** rol de base de datos en la base de datos de destino.  
  
## <a name="establishing-a-sql-azure-connection"></a>Establecimiento de una instancia de SQL Azure conexión  
Para convertir objetos de base de datos de MySQL a sintaxis de SQL Azure, debe establecer una conexión a la instancia de donde van a migrar la base de datos de MySQL o bases de datos de SQL Azure.  
  
Al definir las propiedades de conexión, también se especifique la base de datos que se migrarán los objetos y datos. Puede personalizar esta asignación en el nivel de esquema de MySQL después de conectarse a SQL Azure. Para obtener más información, consulte [asignación de bases de datos de MySQL a SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de intentar conectarse a SQL Azure, asegúrese de la instancia de SQL Azure se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a SQL Azure**  
  
1.  En el **archivo** menú, seleccione **conectarse a SQL Azure** (esta opción se habilita después de la creación de un proyecto).  
  
    Si se ha conectado anteriormente a SQL Azure, el nombre de comando será **volver a conectar a SQL Azure**.  
  
2.  En el cuadro de diálogo de conexión, escriba o seleccione el nombre del servidor de SQL Azure.  
  
3.  Escriba, seleccione o **examinar** el nombre de la base de datos.  
  
4.  Escriba o seleccione **nombre de usuario**.  
  
5.  Escriba el **contraseña**.  
  
6.  SSMA recomienda conexión cifrada a SQL Azure.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para MySQL no admite la conexión a **maestro** base de datos en SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Sincronizar SQL Azure metadatos  
Metadatos acerca de las bases de datos de SQL Azure no se actualizan automáticamente. Los metadatos en el Explorador de metadatos de SQL Azure están una instantánea de los metadatos cuando conectó por primera vez en SQL Azure, o la última vez que usted manualmente han actualizado los metadatos. Puede actualizar manualmente los metadatos para todas las bases de datos, o para cualquier base de datos u objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a SQL Azure.  
  
2.  En el Explorador de metadatos de SQL Azure, active la casilla de verificación junto a la base de datos o el esquema de base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a las bases de datos.  
  
3.  Haga clic en bases de datos, o la base de datos individual o el esquema de base de datos y, a continuación, seleccione **sincronizar con la base de datos**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre los esquemas y las bases de datos de SQL Azure y esquemas de MySQL, vea [bases de datos de asignación de MySQL a SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar las opciones de configuración para los proyectos, vea [establecer las opciones del proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [MySQL de asignación y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Si no tiene que realizar cualquiera de estas tareas, puede convertir las definiciones de objeto de base de datos MySQL en las definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir bases de datos de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
