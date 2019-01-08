---
title: Cargando convertido la base de datos objetos en SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21962c8849204db6f3e5f114b6f8f86994d53b35
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215501"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Cargando convertido la base de datos objetos en SQL Server (DB2ToSQL)
Después de convertir los esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede cargar los objetos de base de datos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos usted mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin modificación, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Ese método es rápido y sencillo, pero no permiten la personalización de la [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de procedimientos almacenados.  
  
Si desea modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] que se utiliza para crear objetos, o si desea más control sobre la creación de objetos, utilice SSMA para crear secuencias de comandos. Puede, a continuación, modificar los scripts, crear cada objeto individualmente e incluso usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Uso de SSMA para crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de base de datos, seleccione los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tal y como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y si están más reciente que el objeto en los metadatos SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], afectará a las definiciones de objeto en SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede cambiar el comportamiento predeterminado mediante la edición **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de objetos que no se han convertido en bases de datos DB2. Sin embargo, esos objetos no se vuelven a crear o modificar SSMA.  
  
**Para sincronizar objetos con SQL Server**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nodo y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a procesar:  
  
    -   Para sincronizar una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o categorías de objetos, active o desactive la casilla de verificación situada junto al objeto o la carpeta.  
  
3.  Una vez haya seleccionado los objetos que se va a procesar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con base de datos**.  
  
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
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar el script, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificación de las secuencias de comandos  
Después de haber guardado el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiciones de objetos como uno o varios scripts, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver y modificar los scripts.  
  
**Para modificar una secuencia de comandos**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, seleccione el archivo de script y, a continuación, haga clic en Aceptar.
  
3.  Editar el archivo de script mediante el editor de consultas.  
  
    Para obtener más información sobre el editor de consultas, vea "Editor comodidad comandos y características" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
4.  Para guardar el script, haga clic en menú archivo **guardar**.  
  
### <a name="running-scripts"></a>Ejecución de Scripts  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para ejecutar un script**  
  
1.  En el [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el **abierto** cuadro de diálogo, seleccione el archivo de script y, a continuación, [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, las instrucciones select en la ventana del editor de consultas y, a continuación, presione el **F5** clave.  
  
Para obtener más información acerca de cómo usar el editor de consultas para ejecutar scripts, vea " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
También puede ejecutar scripts desde la línea de comandos mediante la **sqlcmd** utilidad y desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente, vea "automatizar las tareas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="securing-objects-in-sql-server"></a>Seguridad de los objetos en SQL Server  
Después de haber cargado los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede otorgar y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de cómo ayudar a proteger objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos de DB2 a SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Vea también  
[Migración de datos de DB2 en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
