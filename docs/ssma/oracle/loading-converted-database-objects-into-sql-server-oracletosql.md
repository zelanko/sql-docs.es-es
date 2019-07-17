---
title: Cargando convertido la base de datos objetos en SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 97c34beb0cbe27e8d3c88b922690dc369fb7103b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262988"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Carga de objetos de base de datos convertidos en SQL Server (OracleToSQL)
Después de convertir los esquemas de Oracle a SQL Server, puede cargar los objetos resultantes de la base de datos en SQL Server. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos usted mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de la base de datos de SQL Server.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en SQL Server sin modificación, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Que el método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define los objetos de SQL Server, que no sea de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] que se utiliza para crear objetos, o si desea más control sobre la creación de objetos, utilice SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear cada objeto individualmente e incluso usar el Agente SQL Server para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Para usar SSMA para crear objetos de base de datos de SQL Server, seleccione los objetos en el Explorador de metadatos de SQL Server y, a continuación, sincronice los objetos con SQL Server, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en SQL Server, y si están más reciente que el objeto de SQL Server, los metadatos SSMA SSMA modificará las definiciones de objetos en SQL Server. Puede cambiar el comportamiento predeterminado mediante la edición **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar objetos de base de datos de SQL Server existentes que no se han convertido de bases de datos de Oracle. Sin embargo, esos objetos no se vuelven a crear o modificar SSMA.  
  
**Para sincronizar objetos con SQL Server**  
  
1.  En el Explorador de metadatos de SQL Server, expanda el nodo superior de SQL Server y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a procesar:  
  
    -   Para sincronizar una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o categorías de objetos, active o desactive la casilla de verificación situada junto al objeto o la carpeta.  
  
3.  Una vez haya seleccionado los objetos que se va a procesar en el Explorador de metadatos de SQL Server, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    Después de eso, SSMA mostrará el **sincronizar con base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha ' +' botón. La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de la acción en tres estados:  
  
    -   Una flecha izquierda, significa que el contenido de los metadatos se guardarán en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa que el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Una cruz significa que no se realizará ninguna acción.  
  
Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Para guardar [!INCLUDE[tsql](../../includes/tsql-md.md)] las definiciones de los objetos de base de datos convertida, o para modificar las definiciones de objeto y ejecutar scripts usted mismo, puede guardar la base de datos convertida a las definiciones de objeto [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos.  
  
**Para guardar los objetos como secuencias de comandos**  
  
1.  Una vez haya seleccionado los objetos que se va a guardar en una secuencia de comandos, haga clic en **bases de datos**y, a continuación, haga clic en **Guardar como Script**.  
  
    También puede incluir objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, haga clic en **Guardar como Script**.  
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar el script, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, haga clic en Aceptar SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificación de las secuencias de comandos  
Después de guardar las definiciones de objetos de SQL Server como uno o varios scripts, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver y modificar los scripts.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, seleccione el archivo de script, a continuación, haga clic en Aceptar.
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Editor de comandos y características útiles" en libros en pantalla de SQL Server.  
  
4.  Para guardar el script, haga clic en menú archivo **guardar**.  
  
### <a name="running-scripts"></a>Ejecución de Scripts  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para ejecutar un script**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, seleccione el archivo de script y, a continuación, haga clic en Aceptar  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, las instrucciones select en la ventana del editor de consultas y, a continuación, presione el **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar scripts, vea " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" en libros en pantalla de SQL Server.  
  
También puede ejecutar scripts desde la línea de comandos mediante la **sqlcmd** utilidad y desde el Agente SQL Server. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en libros en pantalla de SQL Server. Para obtener más información acerca del Agente SQL Server, vea "Automatizar tareas administrativas (Agente SQL Server)" en libros en pantalla de SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Seguridad de los objetos en SQL Server  
Después de haber cargado los objetos de base de datos convertida en SQL Server, puede otorgar y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a SQL Server. Para obtener información acerca de cómo proteger los objetos en SQL Server, vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en libros en pantalla de SQL Server.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos a SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
