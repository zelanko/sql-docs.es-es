---
title: Cargar convertido la base de datos objetos en SQL Server (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 5ef463ece76e4077b0c68ba6f1027a516297371c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Cargar convertido la base de datos objetos en SQL Server (OracleToSQL)
Después de haber convertido esquemas de Oracle a SQL Server, puede cargar los objetos de base de datos resultantes en SQL Server. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos por sí mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de la base de datos de SQL Server.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en SQL Server sin modificación, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Que el método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define los objetos de SQL Server, que no sea de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] que se utiliza para crear objetos, o si desea tener mayor control sobre la creación de objetos, use SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear de forma individual cada objeto e incluso usar al Agente SQL Server para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Para usar SSMA para crear objetos de base de datos de SQL Server, seleccione los objetos en el Explorador de metadatos de SQL Server y, a continuación, sincronizar los objetos con SQL Server, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos ya existen en SQL Server y los metadatos SSMA están más reciente que el objeto de SQL Server, SSMA modificará las definiciones de objetos en SQL Server. Puede cambiar el comportamiento predeterminado mediante la edición de **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar los objetos de base de datos de SQL Server existentes que no se han convertido de bases de datos de Oracle. Sin embargo, no se volverá a crearse ni modificar SSMA esos objetos.  
  
**Para sincronizar objetos con SQL Server**  
  
1.  En el Explorador de metadatos de SQL Server, expanda el nodo superior de SQL Server y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos para su procesamiento:  
  
    -   Para sincronizar una base de datos completa, active la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o las categorías de objetos, active o desactive la casilla de verificación situada junto a la carpeta o el objeto.  
  
3.  Después de haber seleccionado los objetos deben procesar en el Explorador de metadatos de SQL Server, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    Después de eso, se mostrará SSMA el **sincronizar con la base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha botón "+". La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de acción en tres estados:  
  
    -   Una flecha izquierda significa que el contenido de los metadatos se guardará en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Un signo de cruz significa que no se van a realizar ninguna acción.  
  
Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con la base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Para guardar [!INCLUDE[tsql](../../includes/tsql_md.md)] las definiciones de los objetos de base de datos convertida, o para cambiar las definiciones de objeto y ejecutar secuencias de comandos por sí mismo, puede guardar la base de datos convertida a las definiciones de objeto [!INCLUDE[tsql](../../includes/tsql_md.md)] secuencias de comandos.  
  
**Para guardar los objetos como secuencias de comandos**  
  
1.  Después de seleccionar los objetos que se va a guardar en una secuencia de comandos, haga clic en **bases de datos**y, a continuación, haga clic en **Guardar como secuencia de comandos**.  
  
    También se pueden incluir objetos individuales o categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, haga clic en **Guardar como secuencia de comandos**.  
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar la secuencia de comandos, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, haga clic en Aceptar SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificar Scripts  
Después de guardar las definiciones de objeto de SQL Server como una o varias secuencias de comandos, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para ver y modificar las secuencias de comandos.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, seleccione el archivo de script, a continuación, haga clic en Aceptar.
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Comodidad comandos y características del Editor" en libros en pantalla de SQL Server.  
  
4.  Para guardar la secuencia de comandos, en el menú, en archivo **guardar**.  
  
### <a name="running-scripts"></a>Ejecutar secuencias de comandos  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para ejecutar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, seleccione el archivo de script y, a continuación, haga clic en Aceptar  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, seleccione las instrucciones en la ventana del editor de consultas y, a continuación, presione la **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar las secuencias de comandos, vea "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" en libros en pantalla de SQL Server.  
  
También puede ejecutar las secuencias de comandos desde la línea de comandos mediante la **sqlcmd** utilidad y desde el Agente SQL Server. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en libros en pantalla de SQL Server. Para obtener más información acerca del agente de SQL Server, vea "Automatizar tareas administrativas (Agente SQL Server)" en libros en pantalla de SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Proteger los objetos de SQL Server  
Después de haber cargado los objetos de base de datos convertida en SQL Server, puede conceder y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a SQL Server. Para obtener información acerca de cómo ayudar a proteger los objetos en SQL Server, vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en libros en pantalla de SQL Server.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [migrar datos a SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
