---
title: Cargando convertido la base de datos objetos en SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5185e8b1364fe2a5bae92c40c99e8f52bcd32ba7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028930"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Carga de objetos de base de datos convertidos en SQL Server (SybaseToSQL)
Después de convertir los objetos de base de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, se pueden cargar los objetos de base de datos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos usted mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o base de datos de SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure sin modificaciones, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Este método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o los objetos de SQL Azure, que no sean de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] que se usa para crear los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, o si desea más control sobre cuándo y cómo se crean los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, use SSMA para crear [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos. Puede, a continuación, modificar los scripts, crear cada objeto individualmente e incluso usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el agente de SQL Azure para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Uso de SSMA para cargar objetos en SQL Server o SQL Azure  
Uso de SSMA para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure, seleccione los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure y si los metadatos SSMA tienen algunos cambios locales o las actualizaciones de la definición de esos objetos muy, SSMA afectará a las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede cambiar el comportamiento predeterminado mediante la edición **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure que no se han convertido de bases de datos de ASE. Sin embargo, esos objetos no se vuelve a crear o modificar SSMA.  
  
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
  
**Para guardar los objetos como secuencias de comandos**  
  
1.  Una vez haya seleccionado los objetos que se va a guardar en una secuencia de comandos, haga clic en **bases de datos**y, a continuación, seleccione **Guardar como Script**.  
  
    También puede incluir objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta contenedora y, a continuación, seleccione **Guardar Script**.  
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar el script, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, haga clic en **Aceptar**.  
  
    SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificación de las secuencias de comandos  
Después de haber guardado el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definiciones de objetos de SQL Azure como uno o varios scripts, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver y modificar los scripts.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, vaya a y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Edición y el archivo de script utilizando el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Editor comodidad comandos y características" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
4.  Para guardar el script, en el menú archivo, seleccione **guardar**.  
  
### <a name="running-scripts"></a>Ejecución de Scripts  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para ejecutar un script**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, vaya a y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, las instrucciones select en la ventana del editor de consultas y, a continuación, presione el **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar scripts, vea " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
También puede ejecutar scripts desde la línea de comandos mediante la **sqlcmd** utilidad y desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente, consulte "automatización de tareas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="securing-objects-in-sql-server"></a>Seguridad de los objetos en SQL Server  
Después de haber cargado los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede otorgar y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de cómo ayudar a proteger objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos de Sybase ASE a SQL Server / SQL Azure(SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
