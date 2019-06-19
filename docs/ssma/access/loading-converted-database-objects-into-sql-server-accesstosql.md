---
title: Cargando convertido la base de datos objetos en SQL Server (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9ab56815fa36f23a15bc646c69094c3ca2f5fa3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299244"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Cargando convertido la base de datos objetos en SQL Server (AccessToSQL)
Después de convertir objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, se pueden cargar los objetos de base de datos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos usted mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o base de datos de SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure sin modificaciones, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Ese método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o los objetos de SQL Azure, que no sean de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] que se utiliza para crear objetos, o si desea más control sobre la creación de objetos, utilice SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear cada objeto individualmente e incluso usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Uso de SSMA para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure, seleccione los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure y si los metadatos SSMA tienen algunos cambios locales o las actualizaciones de la definición de esos objetos muy, SSMA afectará a las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede cambiar el comportamiento predeterminado mediante la edición **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure que no se han convertido de bases de datos de Access. Sin embargo, SSMA no volver a crear o modificar esos objetos.  
  
**Para sincronizar objetos con SQL Server o SQL Azure**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nodo de SQL Azure y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a procesar:  
  
    -   Para sincronizar una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o categorías de objetos, active o desactive la casilla de verificación situada junto al objeto o la carpeta.  
  
3.  Una vez haya seleccionado los objetos que se va a procesar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    Después de eso, SSMA mostrará el **sincronizar con base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha ' +' botón. La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de la acción en tres estados:  
  
    -   Una flecha izquierda, significa que el contenido de los metadatos se guardarán en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa que el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Una cruz significa que no se realizará ninguna acción.  
  
    Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Si desea guardar [!INCLUDE[tsql](../../includes/tsql-md.md)] definiciones de los objetos de base de datos convertida, o bien quiere modificar las definiciones de objetos y ejecutar secuencias de comandos por sí mismo, puede guardar las definiciones de objeto a la base de datos convertida [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos.  
  
**Para guardar uno o más objetos en una secuencia de comandos**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, expanda el nodo superior (el nombre del servidor) y, a continuación, expanda **bases de datos**.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para incluir en script una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para incluir u omitir las vistas individuales, expanda la base de datos, **vistas**y, a continuación, active o desactive la casilla de verificación junto a la vista.  
  
    -   Para incluir u omitir las tablas individuales, expanda la base de datos, **tablas**y, a continuación, active o desactive la casilla de verificación junto a la tabla.  
  
    -   Para incluir u omitir índices individuales para una tabla, expanda la tabla, **índices**y, a continuación, active o desactive el índice.  
  
3.  Haga clic en **bases de datos** y seleccione **Guardar como Script**.  
  
    También puede incluir objetos individuales. Para generar un script un objeto, independientemente de que se seleccionan objetos, haga clic en el objeto y seleccione **Guardar como Script**.  
  
4.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar el script, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, haga clic en **Aceptar**.  
  
    SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificación de las secuencias de comandos  
Después de haber guardado el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definiciones de objetos de SQL Azure como una secuencia de comandos, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para modificar la secuencia de comandos.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Editor comodidad comandos y características" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
4.  Para guardar el script, en el menú archivo, seleccione **guardar**.  
  
### <a name="running-scripts"></a>Ejecución de Scripts  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para ejecutar un script**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto** y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, las instrucciones select en la ventana del editor de consultas y, a continuación, presione el **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar scripts, vea " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
También puede ejecutar scripts desde la línea de comandos mediante la **sqlcmd** utilidad y desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente, vea "automatizar las tareas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="securing-objects-in-sql-server"></a>Seguridad de los objetos en SQL Server  
Después de haber cargado los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede otorgar y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de cómo ayudar a proteger objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos a SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
