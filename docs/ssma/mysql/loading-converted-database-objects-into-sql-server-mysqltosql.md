---
title: Cargando convertido la base de datos objetos en SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b2e58eb534088482493e6f36c3841f36644183af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187229"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>Carga de objetos de base de datos convertidos en SQL Server (MySQLToSQL)
Después de haber convertido las bases de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, se pueden cargar los objetos de base de datos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Se puede tener SSMA crear los objetos, o puede incluir los objetos y ejecutar las secuencias de comandos usted mismo. Además, SSMA permite actualizar los metadatos de destino con el contenido real de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o base de datos de SQL Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elegir entre sincronización y las secuencias de comandos  
Si desea cargar los objetos de base de datos convertida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure sin modificaciones, puede tener SSMA crear o volver a crear los objetos de base de datos directamente. Que el método es rápido y sencillo, pero no permiten la personalización del código de Transact-SQL que define el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de SQL Azure.  
  
Si desea modificar Transact-SQL que se usa para crear objetos, o si desea más control sobre la creación de objetos, use SSMA para crear secuencias de comandos. Puede, a continuación, modificar estos scripts, crear cada objeto individualmente e incluso usar el Agente SQL Server para programar la creación de estos objetos.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Uso de SSMA para sincronizar objetos con SQL Server  
Para usar SSMA para crear objetos de base de datos de SQL Server o SQL Azure, selecciona los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, sincronizar los objetos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, como se muestra en el siguiente procedimiento. De forma predeterminada, si los objetos que ya existen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure y si los metadatos SSMA tienen algunos cambios locales o las actualizaciones de la definición de esos objetos muy, SSMA afectará a las definiciones de objeto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Puede cambiar el comportamiento predeterminado mediante la edición **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure que no se han convertido en bases de datos MySQL. Sin embargo, estos objetos no se vuelven a crear o modificar SSMA.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>Para sincronizar objetos con SQL Server o SQL Azure  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure, expanda la parte superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o nodo de SQL Azure y, a continuación, expanda **bases de datos**.  
  
2.  Seleccione los objetos que se va a procesar:  
  
    -   Para sincronizar una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir los objetos individuales o categorías de objetos, active o desactive la casilla de verificación situada junto al objeto o la carpeta.  
  
3.  Una vez haya seleccionado los objetos que se va a procesar en SQL Server o el Explorador de metadatos de SQL Azure, haga clic en **bases de datos**y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    También puede sincronizar objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    Después de eso, SSMA mostrará el **sincronizar con base de datos** cuadro de diálogo, donde puede ver dos grupos de elementos. En el lado izquierdo, SSMA muestra representados en un árbol de objetos de base de datos seleccionada. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos SSMA. Puede expandir el árbol, haga clic en la izquierda o derecha ' +' botón. La dirección de la sincronización se muestra en la columna de acción que se encuentra entre los dos árboles.  
  
    Puede ser un inicio de sesión de la acción en los tres estados siguientes:  
  
    -   Una flecha izquierda, significa que el contenido de los metadatos se guardarán en la base de datos (el valor predeterminado).  
  
    -   Una flecha derecha significa que el contenido de la base de datos, sobrescribirá los metadatos SSMA.  
  
    -   Una cruz significa que no se realizará ninguna acción.  
  
    -   Haga clic en el signo de acción para cambiar el estado. Sincronización real se realizará al hacer clic en **Aceptar** botón de la **sincronizar con base de datos** cuadro de diálogo.  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Para guardar [!INCLUDE[tsql](../../includes/tsql-md.md)] las definiciones de los objetos de base de datos convertida, o para modificar las definiciones de objeto y ejecutar scripts usted mismo, puede guardar la base de datos convertida a las definiciones de objeto [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos.  
  
**Para guardar los objetos como secuencias de comandos**  
  
1.  Una vez haya seleccionado los objetos que se va a guardar en una secuencia de comandos, haga clic en **bases de datos**y, a continuación, haga clic en **Guardar como Script**.  
  
    También puede incluir objetos individuales o categorías de objetos haciendo clic en el objeto o su carpeta principal y, a continuación, haga clic en **Guardar como Script**.  
  
2.  En el **Guardar como** diálogo cuadro, busque la carpeta donde desea guardar el script, escriba un nombre de archivo en el **nombre de archivo** cuadro y, a continuación, [!INCLUDE[clickOK](../../includes/clickok-md.md)] SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificación de las secuencias de comandos  
Después de haber guardado como un script de SQL Server o las definiciones de objetos de SQL Azure, puede usar SQL Server Management Studio para modificar el script.  
  
**Para modificar una secuencia de comandos**  
  
1.  En Management Studio **archivo** menú, elija **abierto**y, a continuación, haga clic en **archivo**.  
  
2.  En el cuadro de diálogo Abrir, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Editar el archivo de script mediante el editor de consultas. Para obtener más información sobre el editor de consultas, vea "Editor de comandos y características útiles" en libros en pantalla de SQL Server.  
  
4.  Para guardar el script, en el menú archivo, seleccione **guardar**.  
  
### <a name="running-scripts"></a>Ejecución de Scripts  
Puede ejecutar una secuencia de comandos o instrucciones individuales, en SQL Server Management Studio.  
  
**Para ejecutar un script**  
  
1.  En SQL Server Management Studio **archivo** menú, elija **abierto** y, a continuación, haga clic en **archivo**.  
  
2.  En el cuadro de diálogo Abrir, busque y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione el **F5** clave.  
  
4.  Para ejecutar un conjunto de instrucciones, las instrucciones select en la ventana del editor de consultas y, a continuación, presione el **F5** clave.  
  
5.  Para obtener más información acerca de cómo usar el editor de consultas para ejecutar scripts, vea "SQL Server Management Studio Transact-SQL Query" en libros en pantalla de SQL Server.  
  
6.  También puede ejecutar scripts desde la línea de comandos mediante la **sqlcmd** utilidad y del Agente SQL Server. Para obtener más información acerca de **sqlcmd**, vea "utilidad sqlcmd" en libros en pantalla de SQL Server. Para obtener más información acerca del Agente SQL Server, vea "Automatizar tareas administrativas (Agente SQL Server)" en libros en pantalla de SQL Server.  
  
## <a name="securing-objects-in-sql-server"></a>Seguridad de los objetos en SQL Server  
Después de haber cargado los objetos de base de datos convertida en SQL Server, puede otorgar y denegar permisos en estos objetos. Es una buena idea hacerlo antes de migrar datos a SQL Server. Para obtener información acerca de cómo proteger los objetos en SQL Server, vea "Consideraciones para las bases de datos y base de datos de aplicaciones de seguridad" en libros en pantalla de SQL Server.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [migrar datos de MySQL a SQL Server: Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
