---
title: Conexión a Azure SQL DB (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 10be1dc3652c944b9de08a01b0f4cdff5ae5849a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176241"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conexión a Azure SQL DB (SybaseToSQL)
Para migrar bases de datos de Sybase a Azure SQL DB, debe conectarse a la instancia de destino de Azure SQL DB. Cuando se conecta, SSMA obtiene los metadatos de todas las bases de datos de la instancia de Azure SQL Database y muestra los metadatos de la base de datos en el explorador de metadatos de Azure SQL DB. SSMA almacena información de la instancia de Azure SQL DB a la que está conectado, pero no almacena contraseñas.  
  
La conexión a Azure SQL DB permanece activa hasta que se cierra el proyecto. Cuando vuelva a abrir el proyecto, debe volver a conectarse a Azure SQL DB si desea una conexión activa con el servidor. Puede trabajar sin conexión hasta que cargue los objetos de base de datos en Azure SQL DB y migre los datos.  
  
Los metadatos sobre la instancia de Azure SQL DB no se sincronizan automáticamente. En su lugar, para actualizar los metadatos en el explorador de metadatos de Azure SQL Database, debe actualizar manualmente los metadatos de la base de datos SQL de Azure. Para obtener más información, vea la sección "sincronización de metadatos de Azure SQL DB" más adelante en este tema.  
  
## <a name="required-azure-sql-db-permissions"></a>Permisos necesarios de Azure SQL Database  
La cuenta que se usa para conectarse a Azure SQL DB requiere permisos diferentes en función de las acciones que realiza la cuenta:  
  
1.  Para convertir objetos de Sybase [!INCLUDE[tsql](../../includes/tsql-md.md)] en sintaxis, actualizar metadatos de Azure SQL dB o guardar la sintaxis convertida en scripts, la cuenta debe tener permiso para iniciar sesión en la instancia de base de datos SQL de Azure.  
  
2.  Para cargar objetos de base de datos en Azure SQL DB, el requisito de permiso mínimo es la pertenencia al rol de base de datos **db_owner** en la base de datos de destino.  
  
## <a name="establishing-an-azure-sql-db-connection"></a>Establecimiento de una conexión a Azure SQL DB  
Antes de convertir los objetos de base de datos de Sybase a la sintaxis de Azure SQL Database, debe establecer una conexión con la instancia de base de datos SQL de Azure en la que desea migrar la base de datos o las bases de datos de Sybase.  
  
Al definir las propiedades de conexión, también se especifica la base de datos en la que se migrarán los objetos y los datos. Puede personalizar esta asignación en el nivel de esquema de Sybase después de conectarse a Azure SQL DB. Para obtener más información, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de intentar conectarse a Azure SQL DB, asegúrese de que la instancia de Azure SQL DB se está ejecutando y puede aceptar conexiones.  
  
**Para conectarse a Azure SQL DB**  
  
1.  En el menú **archivo** , seleccione **conectarse a Azure SQL dB**(esta opción se habilita después de la creación de un proyecto).  
  
    Si previamente se ha conectado a Azure SQL DB, el nombre del comando se volverá **a conectar a Azure SQL dB**  
  
2.  En el cuadro de diálogo conexión, escriba o seleccione el nombre del servidor de Azure SQL DB.  
  
3.  Escriba, seleccione o **examine** el nombre de la base de datos.  
  
4.  Escriba o seleccione el **nombre de usuario**.  
  
5.  Escriba la **contraseña**.  
  
6.  SSMA recomienda una conexión cifrada a Azure SQL DB.  
  
7.  Haga clic en **Conectar**.  
  
> [!IMPORTANT]  
> SSMA para Sybase no admite la conexión a la base de datos **maestra** en Azure SQL dB.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronización de metadatos de Azure SQL DB  
Los metadatos acerca de las bases de datos de base de datos SQL de Azure no se actualizan automáticamente. Los metadatos del explorador de metadatos de Azure SQL Database son una instantánea de los metadatos la primera vez que se conecta a Azure SQL DB o la última vez que se actualizaron los metadatos manualmente. Puede actualizar manualmente los metadatos de todas las bases de datos o de cualquier base de datos o objeto de base de datos.  
  
**Para sincronizar los metadatos**  
  
1.  Asegúrese de que está conectado a Azure SQL DB.  
  
2.  En el explorador de metadatos de Azure SQL Database, active la casilla situada junto a la base de datos o el esquema de la base de datos que desea actualizar.  
  
    Por ejemplo, para actualizar los metadatos de todas las bases de datos, active la casilla situada junto a bases de datos.  
  
3.  Haga clic con el botón derecho en bases de datos o en el esquema de base de datos o de base de datos individual y seleccione **sincronizar con base de datos**.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación entre los esquemas de Sybase y las bases de datos y los esquemas de Azure SQL Database, consulte [asignación de esquemas de Sybase ase a esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar las opciones de configuración de los proyectos, vea [establecer opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, consulte [asignación de tipos de datos de Sybase ase y SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Si no tiene que realizar ninguna de estas tareas, puede convertir las definiciones de objetos de base de datos de Sybase en definiciones de objetos de Azure SQL DB. Para obtener más información, consulte [conversión de objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de Sybase ASE a SQL Server: Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
