---
title: Cargar convertido la base de datos objetos en SQL Server (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
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
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2d3aa3c367ee065fb04dbe828003d0a2fa304e08
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Cargar convertido la base de datos objetos en SQL Server (AccessToSQL)
Después de convertir objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, puede cargar los objetos de base de datos resultante en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos por sí mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure sin modificaciones, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Ese método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure, que no sea de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] que se utiliza para crear objetos, o si desea tener mayor control sobre la creación de objetos, use SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear de forma individual cada objeto e incluso [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Usar SSMA para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure, seleccione los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y si los metadatos SSMA tiene algunos cambios locales o las actualizaciones de la definición de esos objetos muy, SSMA modificará las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Puede cambiar el comportamiento predeterminado mediante la edición de **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure que no se han convertido de bases de datos de Access. Sin embargo, SSMA no volver a crear o modificar esos objetos.  
  
**Para sincronizar objetos con SQL Server o SQL Azure**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o nodo de SQL Azure y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos para su procesamiento:  
  
    -   Para sincronizar una base de datos completa, active la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o las categorías de objetos, active o desactive la casilla de verificación situada junto a la carpeta o el objeto.  
  
3.  Después de seleccionar los objetos para procesar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    Después de eso, se mostrará SSMA el **sincronizar con la base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha botón "+". La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de acción en tres estados:  
  
    -   Una flecha izquierda significa que el contenido de los metadatos se guardará en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Un signo de cruz significa que no se van a realizar ninguna acción.  
  
    Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con la base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Si desea guardar [!INCLUDE[tsql](../../includes/tsql_md.md)] las definiciones de los objetos de base de datos convertida y desea modificar las definiciones de objeto y ejecutar secuencias de comandos por sí mismo, puede guardar las definiciones de objeto a la base de datos convertida [!INCLUDE[tsql](../../includes/tsql_md.md)] secuencias de comandos.  
  
**Para guardar uno o varios objetos en una secuencia de comandos**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, expanda el nodo superior (el nombre del servidor) y, a continuación, **bases de datos**.  
  
2.  Realice uno o varios de los procedimientos siguientes:  
  
    -   Para una base de datos completa en el script, seleccione la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para generar un script u Omitir vistas individuales, expanda la base de datos, **vistas**y, a continuación, active o desactive la casilla de verificación situada junto a la vista.  
  
    -   Para generar un script u omite las tablas individuales, expanda la base de datos, **tablas**y, a continuación, active o desactive la casilla situada junto a la tabla.  
  
    -   Para generar un script u Omitir índices individuales para una tabla, expanda la tabla, **índices**y, a continuación, active o desactive el índice.  
  
3.  Haga clic en **bases de datos** y seleccione **Guardar como secuencia de comandos**.  
  
    También puede incluir objetos individuales. Para generar un script un objeto, con independencia de qué objetos están seleccionados, haga clic en el objeto y seleccione **Guardar como secuencia de comandos**.  
  
4.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar la secuencia de comandos, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, haga clic en **Aceptar**.  
  
    SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificar Scripts  
Después de haber guardado la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o definiciones de objetos de SQL Azure como una secuencia de comandos, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para modificar la secuencia de comandos.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Comodidad comandos y características del Editor" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
4.  Para guardar la secuencia de comandos, en el menú archivo, seleccione **guardar**.  
  
### <a name="running-scripts"></a>Ejecutar secuencias de comandos  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para ejecutar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **archivo** menú, elija **abiertos** y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, seleccione las instrucciones en la ventana del editor de consultas y, a continuación, presione la **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar las secuencias de comandos, vea "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
También puede ejecutar las secuencias de comandos desde la línea de comandos mediante la **sqlcmd** utilidad y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente, vea "automatizar las tareas administrativas ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="securing-objects-in-sql-server"></a>Proteger los objetos de SQL Server  
Después de haber cargado los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede conceder y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener información acerca de cómo ayudar a proteger los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos a SQL Server](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
