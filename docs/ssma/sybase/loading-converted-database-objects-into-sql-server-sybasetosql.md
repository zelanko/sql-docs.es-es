---
title: Carga de objetos de base de datos convertidos en SQL Server (SybaseToSQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028930"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Carga de objetos de base de datos convertidos en SQL Server (SybaseToSQL)
Después de haber convertido los objetos de base de datos de Sybase Adaptive Server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise (ASE) en o SQL Azure, puede cargar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos de base de datos resultantes en o SQL Azure. Puede hacer que SSMA cree los objetos, o bien puede crear un script de los objetos y ejecutar los scripts usted mismo. Además, SSMA le permite actualizar los metadatos de destino con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenido real de o SQL Azure base de datos.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Elección entre sincronización y scripts  
Si desea cargar los objetos de base de datos convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure sin modificaciones, puede hacer que SSMA cree directamente o vuelva a crear los objetos de base de datos. Este método es rápido y sencillo, pero no permite la [!INCLUDE[tsql](../../includes/tsql-md.md)] personalización del código que define los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos o SQL Azure, excepto los procedimientos almacenados.  
  
Si [!INCLUDE[tsql](../../includes/tsql-md.md)] desea modificar el objeto que se usa para crear los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, o si desea tener más control sobre cuándo y cómo se crean los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, utilice SSMA para crear [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts. Después, puede modificar esos scripts, crear cada objeto individualmente e, incluso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usar o SQL Azure agente para programar la creación de esos objetos.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Usar SSMA para cargar objetos en SQL Server o SQL Azure  
Para usar SSMA con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fin de crear o SQL Azure objetos de base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione los objetos en o SQL Azure explorador de metadatos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, a continuación, sincronice los objetos con o SQL Azure, como se muestra en el procedimiento siguiente. De forma predeterminada, si los objetos ya existen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en o SQL Azure, y si los metadatos de SSMA tienen algún cambio local o actualizaciones de la definición de esos objetos muy, SSMA modificará las definiciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de objetos en o SQL Azure. Puede cambiar el comportamiento predeterminado editando la **configuración del proyecto**.  
  
> [!NOTE]  
> Puede seleccionar objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de SQL Azure o existentes que no se hayan convertido de bases de datos de ase. No obstante, SSMA no volverá a crear ni modificar esos objetos.  
  
**Para sincronizar objetos con SQL Server o SQL Azure**  
  
1.  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure explorador de metadatos, expanda el nodo superior [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure y, a continuación, expanda **bases**de datos.  
  
2.  Seleccionar los objetos que se van a procesar:  
  
    -   Para sincronizar una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para sincronizar u omitir objetos o categorías de objetos individuales, Active o desactive la casilla situada junto al objeto o la carpeta.  
  
3.  Una vez que haya seleccionado los objetos que desea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesar en el explorador de metadatos o SQL Azure, haga clic con el botón secundario en **bases**de datos y, a continuación, haga clic en **sincronizar con base**de datos.  
  
    También puede sincronizar objetos individuales o categorías de objetos; para ello, haga clic con el botón secundario en el objeto o en su carpeta primaria y, a continuación, haga clic en **sincronizar con base de datos**.  
  
    Después, SSMA mostrará el cuadro de diálogo **sincronizar con base de datos** , donde podrá ver dos grupos de elementos. En el lado izquierdo, SSMA muestra los objetos de base de datos seleccionados representados en un árbol. En el lado derecho, puede ver un árbol que representa los mismos objetos en los metadatos de SSMA. Para expandir el árbol, haga clic en el botón de la derecha o la izquierda ' + '. La dirección de la sincronización se muestra en la columna Acción situada entre los dos árboles.  
  
    Un signo de acción puede tener tres Estados:  
  
    -   Una flecha izquierda significa que el contenido de los metadatos se guardará en la base de datos (valor predeterminado).  
  
    -   Una flecha A la derecha significa que el contenido de la base de datos sobrescribirá los metadatos de SSMA.  
  
    -   Un signo cruzado significa que no se realizará ninguna acción.  
  
Haga clic en el signo de acción para cambiar el estado. La sincronización real se realizará al hacer clic en el botón **Aceptar** del cuadro de diálogo **sincronizar con base de datos** .  
  
## <a name="scripting-objects"></a>Objetos de scripting  
Si desea guardar [!INCLUDE[tsql](../../includes/tsql-md.md)] definiciones de los objetos de base de datos convertidos, o si desea modificar las definiciones de objeto y ejecutar scripts usted mismo, puede guardar las definiciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] objetos de base de datos convertidas en scripts.  
  
**Para guardar objetos como scripts**  
  
1.  Una vez que haya seleccionado los objetos que desea guardar en un script, haga clic con el botón derecho en **bases de datos**y, a continuación, seleccione **Guardar como script**.  
  
    También puede incluir en el script objetos individuales o categorías de objetos; para ello, haga clic con el botón secundario en el objeto o en la carpeta que lo contiene y seleccione **Guardar script**.  
  
2.  En el cuadro de diálogo **Guardar como** , busque la carpeta en la que desea guardar el script, escriba un nombre de archivo en el cuadro **nombre de archivo** y, a continuación, haga clic en **Aceptar**.  
  
    SSMA anexará la extensión de nombre de archivo. SQL.  
  
### <a name="modifying-scripts"></a>Modificar scripts  
Una vez guardadas las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiciones de objeto o SQL Azure como uno o varios scripts, puede [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usar para ver y modificar los scripts.  
  
**Para modificar un script**  
  
1.  En el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Archivo** , seleccione **Abrir**y haga clic en **Archivo**.  
  
2.  En el cuadro de diálogo **abrir** , vaya a y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Edite y el archivo de script mediante el editor de consultas.  
  
    Para obtener más información acerca del editor de consultas, vea el tema sobre los comandos y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las características de la comodidad del editor en los libros en pantalla de.  
  
4.  Para guardar el script, en el menú Archivo, seleccione **Guardar**.  
  
### <a name="running-scripts"></a>Ejecutar scripts  
Puede ejecutar un script, o instrucciones individuales, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
**Para ejecutar un script**  
  
1.  En el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Archivo** , seleccione **Abrir**y haga clic en **Archivo**.  
  
2.  En el cuadro de diálogo **abrir** , vaya a y seleccione el archivo de script y, a continuación, haga clic en **Aceptar**.  
  
3.  Para ejecutar el script completo, presione la tecla **F5** .  
  
4.  Para ejecutar un conjunto de instrucciones, seleccione las instrucciones en la ventana del editor de consultas y, a continuación, presione la tecla **F5** .  
  
Para obtener más información sobre cómo usar el editor de consultas de para ejecutar scripts [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] , vea " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consulta" en los libros en pantalla de.  
  
También puede ejecutar scripts desde la línea de comandos mediante la utilidad **sqlcmd** y desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el agente. Para obtener más información sobre **sqlcmd**, vea "utilidad SQLCMD" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los libros en pantalla de. Para obtener más información [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acerca del agente, vea "automatizar tareas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrativas (agente) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " en los libros en pantalla de.  
  
## <a name="securing-objects-in-sql-server"></a>Proteger objetos en SQL Server  
Una vez cargados los objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos convertidos en, puede conceder y denegar permisos en esos objetos. Es una buena idea hacerlo antes de migrar los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre cómo proteger objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "consideraciones de seguridad para bases de datos y aplicaciones de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos" en los libros en pantalla de.  
  
## <a name="next-step"></a>siguiente paso  
El siguiente paso del proceso de migración consiste en [migrar los datos de Sybase ase a SQL Server/SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de Sybase ASE a SQL Server: Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
