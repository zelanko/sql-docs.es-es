---
title: Trabajar con proyectos de SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 37a763c0acca891d8bbbc1a310edcb6f8b987436
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904903"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Proyectos de SSMA (MySQLToSQL)
Para migrar bases de datos MySQL a SQL Server o SQL Azure, primero debe crear un proyecto de SSMA. El proyecto es un archivo que contiene la información siguiente:  
  
-   Metadatos acerca de las bases de datos MySQL que se van a migrar a SQL Server o SQL Azure.  
  
-   Metadatos acerca de la instancia de SQL Server o SQL Azure que va a recibir los objetos migrados y los datos de destino.  
  
-   Información de conexión de SQL Server o SQL Azure.  
  
-   Configuración del proyecto.  
  
Al abrir un proyecto, se desconecta de MySQL y SQL Server o SQL Azure. Que le permite trabajar sin conexión. Para obtener más información sobre cómo volver a conectarse a SQL Server, vea [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y cargar la base de datos, migración de datos y sincronización SSMA con MySQL y SQL Server o SQL Azure. Los valores predeterminados son adecuados para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar la configuración. Si es necesario, puede cambiar la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
##### <a name="to-review-default-project-settings"></a>Para revisar la configuración predeterminada del proyecto  
  
1.  Seleccione **la configuración predeterminada del proyecto** desde el **herramientas** menú.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a qué opciones de configuración se pueden ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revisar y cambiar la configuración según sea necesario. Para obtener más información sobre estas opciones, consulte [configuración del proyecto &#40;conversión&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Repita los pasos 1 a 3 para la migración, la sincronización, SQL Azure, interfaz gráfica de usuario y asignación de tipos de páginas.  
  
-   Para obtener información acerca de la configuración de la migración, consulte [configuración del proyecto &#40;migración&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Para obtener información sobre la configuración de sincronización a SQL Server, vea [configuración del proyecto &#40;sincronización&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Para obtener información acerca de la configuración de la interfaz gráfica de usuario, consulte [configuración de proyecto (GUI) (SSMA comunes)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Para obtener información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto &#40;asignación de tipo&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Para obtener información acerca de la configuración de SQL Azure, consulte [configuración del proyecto &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> Se mostrará la configuración de SQL Azure solo cuando se selecciona **migración a SQL Azure** al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Creación de nuevos proyectos  
Para migrar datos desde bases de datos MySQL a SQL Server o SQL Azure, debe crear un proyecto.  
  
##### <a name="to-create-a-new-project"></a>Para crear un nuevo proyecto  
  
1.  Seleccione **nuevo proyecto** desde el **archivo** menú. Aparecerá el cuadro de diálogo **Nuevo proyecto** . En el menú **Archivo**, seleccione **Nuevo proyecto**. Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** , escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
4.  En el **migración a** lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL DB  
  
Y, a continuación, haga clic en **Aceptar**  
  
SSMA crea el archivo de proyecto.  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir el valor predeterminado configuración del proyecto que se aplica a los nuevos proyectos SSMA también puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [definir opciones de proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Al personalizar asignaciones de tipos de datos entre las bases de datos de origen y destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información, consulte [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Guardando proyectos  
La característica de guardar proyectos permite al usuario guardar esencialmente la configuración del proyecto y, opcionalmente, los metadatos de la base de datos en el archivo del proyecto SSMA.  
  
##### <a name="to-save-a-project"></a>Para guardar un proyecto  
  
-   En el **archivo** menú, seleccione **guardar** proyecto.  
  
Si las bases de datos dentro del proyecto han cambiado o no se han convertido, SSMA le pedirá que cargue y guarde los metadatos. Cargar y guardar los metadatos le permiten trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, como el personal de soporte técnico. Si se le pedirá que guarde los metadatos, realice lo siguiente:  
  
1.  Para cada base de datos que muestra el estado **donde faltan metadatos**, active la casilla situada junto al nombre de la base de datos. Guardar metadatos podría tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
2.  Haga clic en **Guardar**.  
  
SSMA analizará los esquemas de MySQL y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Al abrir un proyecto, se desconecta de MySQL y de SQL Server o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos de SQL Server o SQL Azure. Para migrar datos, debe volver a conectarse a SQL Server o SQL Azure.  
  
##### <a name="to-open-a-project"></a>Para abrir un proyecto  
  
1.  Realice uno de los siguientes procedimientos:  
  
    1.  En el **archivo** menú, elija **proyectos recientes**.  
  
    2.  Seleccione el proyecto que desea abrir.  
  
    3.  En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .m2ssproj, seleccione el archivo y, a continuación, haga clic en **abierto**.  
  
2.  Para volver a conectarse a MySQL, en el **archivo** menú, seleccione **volver a conectar con MySQL**.  
  
3.  Para volver a conectarse a SQL Server, en el **archivo** menú, seleccione **volver a conectar a SQL Server**.  
  
4.  Para volver a conectarse a SQL Azure, en el **archivo** menú, seleccione **volver a conectarse a SQL Azure.**  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Conexión a Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
