---
title: Cargar convertido la base de datos objetos en SQL Server (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dce262249789e1b7335b1af0d8576239747d5347
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>Cargar convertido la base de datos objetos en SQL Server (MySQLToSQL)
Después de haber convertido las bases de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, puede cargar los objetos de base de datos resultante en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos por sí mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure sin modificaciones, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Que el método es rápido y sencillo, pero no permiten la personalización del código de Transact-SQL que define la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure.  
  
Si desea modificar Transact-SQL que se utiliza para crear objetos, o si desea tener más control sobre la creación de objetos, use SSMA para crear secuencias de comandos. Puede modificar, a continuación, estas secuencias de comandos, crear de forma individual cada objeto e incluso usar al Agente SQL Server para programar la creación de estos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Para usar SSMA para crear objetos de base de datos de SQL Server o SQL Azure, seleccione los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y si los metadatos SSMA tiene algunos cambios locales o las actualizaciones de la definición de esos objetos muy, SSMA modificará las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Puede cambiar el comportamiento predeterminado mediante la edición de **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure que no se han convertido de bases de datos de MySQL. Sin embargo, estos objetos no se vuelven a crear o modificar SSMA.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>Para sincronizar objetos con SQL Server o SQL Azure  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o nodo de SQL Azure y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos para su procesamiento:  
  
    -   Para sincronizar una base de datos completa, active la casilla de verificación situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o las categorías de objetos, active o desactive la casilla de verificación situada junto a la carpeta o el objeto.  
  
3.  Después de seleccionar los objetos para procesar en SQL Server o en el Explorador de metadatos de SQL Azure, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con la base de datos**.  
  
    Después de eso, se mostrará SSMA el **sincronizar con la base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha botón "+". La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de acción en los tres estados siguientes:  
  
    -   Una flecha izquierda significa que el contenido de los metadatos se guardará en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Un signo de cruz significa que no se van a realizar ninguna acción.  
  
    -   Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con la base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Para guardar [!INCLUDE[tsql](../../includes/tsql_md.md)] las definiciones de los objetos de base de datos convertida, o para cambiar las definiciones de objeto y ejecutar secuencias de comandos por sí mismo, puede guardar la base de datos convertida a las definiciones de objeto [!INCLUDE[tsql](../../includes/tsql_md.md)] secuencias de comandos.  
  
**Para guardar los objetos como secuencias de comandos**  
  
1.  Después de seleccionar los objetos que se va a guardar en una secuencia de comandos, haga clic en **bases de datos**y, a continuación, haga clic en **Guardar como secuencia de comandos**.  
  
    También se pueden incluir objetos individuales o categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, haga clic en **Guardar como secuencia de comandos**.  
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar la secuencia de comandos, escriba un nombre de archivo en el **nombre de archivo** (cuadro) y, a continuación, [!INCLUDE[clickOK](../../includes/clickok_md.md)] SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificar Scripts  
Después de haber guardado el SQL Server o definiciones de objetos de SQL Azure como una secuencia de comandos, puede usar SQL Server Management Studio para modificar la secuencia de comandos.  
  
**Para modificar una secuencia de comandos**  
  
1.  En Management Studio **archivo** menú, elija **abiertos**y, a continuación, haga clic en **archivo**.  
  
2.  En el cuadro de diálogo Abrir, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Editar el archivo de script mediante el editor de consultas. Para obtener más información sobre el editor de consultas, vea "Comodidad comandos y características del Editor" en libros en pantalla de SQL Server.  
  
4.  Para guardar la secuencia de comandos, en el menú archivo, seleccione **guardar**.  
  
### <a name="running-scripts"></a>Ejecutar secuencias de comandos  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en SQL Server Management Studio.  
  
**Para ejecutar una secuencia de comandos**  
  
1.  En SQL Server Management Studio **archivo** menú, elija **abiertos** y, a continuación, haga clic en **archivo**.  
  
2.  En el cuadro de diálogo Abrir, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, seleccione las instrucciones en la ventana del editor de consultas y, a continuación, presione la **F5** clave.  
  
5.  Para obtener más información acerca de cómo usar el editor de consultas para ejecutar las secuencias de comandos, vea "SQL Server Management Studio consulta Transact-SQL" en libros en pantalla de SQL Server.  
  
6.  También puede ejecutar las secuencias de comandos desde la línea de comandos mediante la **sqlcmd** utilidad y del Agente SQL Server. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en libros en pantalla de SQL Server. Para obtener más información acerca del agente de SQL Server, vea "Automatizar tareas administrativas (Agente SQL Server)" en libros en pantalla de SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Proteger los objetos de SQL Server  
Después de haber cargado los objetos de base de datos convertida en SQL Server, puede conceder y denegar permisos en estos objetos. Es una buena idea hacerlo antes de migrar datos a SQL Server. Para obtener información acerca de cómo ayudar a proteger los objetos en SQL Server, vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en libros en pantalla de SQL Server.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos de MySQL a SQL Server: base de datos de SQL de Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

