---
title: Cargar convertido la base de datos objetos en SQL Server (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
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
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 04d7ce18baed888af7b0de96faec99b72a6b4586
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Cargar convertido la base de datos objetos en SQL Server (DB2ToSQL)
Después de haber convertido esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede cargar los objetos de base de datos resultante en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos por sí mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sin modificación, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Ese método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql_md.md)] código que define la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, distintos de los procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] que se utiliza para crear objetos, o si desea tener mayor control sobre la creación de objetos, use SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear de forma individual cada objeto e incluso [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Usar SSMA para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de base de datos, seleccione los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], tal y como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y si los metadatos SSMA están más reciente que el objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA modificará las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Puede cambiar el comportamiento predeterminado mediante la edición de **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos de objetos que no se han convertido de bases de datos DB2. Sin embargo, no se volverá a crearse ni modificar SSMA esos objetos.  
  
**Para sincronizar objetos con SQL Server**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nodo y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos para su procesamiento:  
  
    -   Para sincronizar una base de datos completa, active la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o las categorías de objetos, active o desactive la casilla de verificación situada junto a la carpeta o el objeto.  
  
3.  Después de seleccionar los objetos para procesar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
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
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar la secuencia de comandos, escriba un nombre de archivo en el **nombre de archivo** (cuadro) y, a continuación, [!INCLUDE[clickOK](../../includes/clickok_md.md)]. SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificar Scripts  
Después de haber guardado la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiciones de objetos como uno o más scripts, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para ver y modificar las secuencias de comandos.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, seleccione el archivo de script y, a continuación, haga clic en Aceptar.
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Comodidad comandos y características del Editor" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
4.  Para guardar la secuencia de comandos, en el menú, en archivo **guardar**.  
  
### <a name="running-scripts"></a>Ejecutar secuencias de comandos  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Para ejecutar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abiertos** cuadro de diálogo, seleccione el archivo de script y, a continuación, [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, seleccione las instrucciones en la ventana del editor de consultas y, a continuación, presione la **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar las secuencias de comandos, vea "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] consulta" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
También puede ejecutar las secuencias de comandos desde la línea de comandos mediante la **sqlcmd** utilidad y desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente, vea "automatizar las tareas administrativas ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] agente)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="securing-objects-in-sql-server"></a>Proteger los objetos de SQL Server  
Después de haber cargado los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede conceder y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener información acerca de cómo ayudar a proteger los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [migrar datos de DB2 en SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de DB2 en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
