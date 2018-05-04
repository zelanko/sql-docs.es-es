---
title: Trabajar con proyectos SSMA (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 00ae7a95cd9574878caa46ed13d6b8c30a898c07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Trabajar con proyectos SSMA (MySQLToSQL)
Para migrar las bases de datos de MySQL a SQL Server o SQL Azure, primero debe crear un proyecto SSMA. El proyecto es un archivo que contiene la información siguiente:  
  
-   Metadatos acerca de las bases de datos de MySQL que se van a migrar a SQL Server o SQL Azure.  
  
-   Metadatos acerca de la instancia de destino de SQL Server o SQL Azure que recibirá los objetos migrados y los datos.  
  
-   Información de conexión de SQL Server o SQL Azure.  
  
-   Configuración del proyecto.  
  
Cuando se abre un proyecto, se desconecta de MySQL y SQL Server o SQL Azure. Que le permite trabajar sin conexión. Para obtener más información acerca de cómo volver a conectarse a SQL Server, vea [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de configuración de conversión y cargar la base de datos, migrar datos y sincronización de SSMA con MySQL y SQL Server o SQL Azure. Los valores predeterminados son adecuados para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debería revisar la configuración. Si es necesario, puede cambiar la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
##### <a name="to-review-default-project-settings"></a>Para revisar la configuración predeterminada del proyecto  
  
1.  Seleccione **la configuración predeterminada del proyecto** desde el **herramientas** menú.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a los valores que se van a ver / cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revisar y cambiar la configuración según sea necesario. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto &#40;conversión&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Repita los pasos 1 a 3 para las páginas de la migración, la sincronización, SQL Azure, interfaz gráfica de usuario y asignación de tipo.  
  
-   Para obtener información acerca de la configuración de la migración, consulte [configuración del proyecto &#40;migración&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Para obtener información sobre la configuración de sincronización a SQL Server, vea [configuración del proyecto &#40;sincronización&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Para obtener información acerca de la configuración de la interfaz gráfica de usuario, consulte [configuración de proyecto (GUI) (SSMA común)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Para obtener información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto &#40;asignación de tipos de&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Para obtener información acerca de la configuración de SQL Azure, consulte [configuración del proyecto &#40;base de datos de SQL Azure&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> Se mostrará la configuración de SQL Azure solo cuando se selecciona **migración a SQL Azure** al crear un proyecto.  
  
## <a name="creating-new-projects"></a>Crear nuevos proyectos  
Para migrar datos desde bases de datos de MySQL a SQL Server o SQL Azure, debe crear un proyecto.  
  
##### <a name="to-create-a-new-project"></a>Para crear un nuevo proyecto  
  
1.  Seleccione **nuevo proyecto** desde el **archivo** menú. Aparecerá el cuadro de diálogo **Nuevo proyecto** . En el menú **Archivo**, seleccione **Nuevo proyecto**. Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto.  
  
4.  En el **migración a** de lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Base de datos de SQL Azure  
  
Y, a continuación, haga clic en **Aceptar**  
  
SSMA crea el archivo de proyecto.  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir el valor predeterminado configuración del proyecto que se aplican a todos los nuevos proyectos SSMA también puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [establecer las opciones del proyecto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Si desea personalizar asignaciones de tipos de datos entre las bases de datos de origen y de destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información, consulte [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Guardar proyectos  
La característica de guardar proyectos permite al usuario guardar básicamente la configuración del proyecto y, opcionalmente, los metadatos de la base de datos en el archivo de proyecto SSMA.  
  
##### <a name="to-save-a-project"></a>Para guardar un proyecto  
  
-   En el **archivo** menú, seleccione **guardar** proyecto.  
  
Si las bases de datos dentro del proyecto han cambiado o que no se ha convertido, SSMA le pedirá que para cargar y guardar los metadatos. Cargar y guardar los metadatos le permite trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, como el personal de soporte técnico. Si le pide que guarde los metadatos, realice lo siguiente:  
  
1.  Para cada base de datos que muestra un estado de **faltan metadatos**, active la casilla situada junto al nombre de la base de datos. Guardar los metadatos puede tardar varios minutos. Si no desea guardar los metadatos en este momento, no seleccione las casillas de verificación.  
  
2.  Haga clic en **Guardar**.  
  
SSMA analizará los esquemas de MySQL y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Cuando se abre un proyecto, se desconecta de MySQL y de SQL Server o SQL Azure. Esto le permite trabajar sin conexión. Para actualizar los metadatos, cargará los objetos de base de datos en SQL Server o SQL Azure. Para migrar datos, debe volver a conectarse a SQL Server o SQL Azure.  
  
##### <a name="to-open-a-project"></a>Para abrir un proyecto  
  
1.  Realice uno de los siguientes procedimientos:  
  
    1.  En el **archivo** menú, elija **proyectos recientes**.  
  
    2.  Seleccione el proyecto que desea abrir.  
  
    3.  En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .m2ssproj, seleccione el archivo y, a continuación, haga clic en **abiertos**.  
  
2.  Volver a conectar con MySQL, en la **archivo** menú, seleccione **volver a conectar con MySQL**.  
  
3.  Para volver a conectarse a SQL Server, en la **archivo** menú, seleccione **volver a conectar a SQL Server**.  
  
4.  Para volver a conectarse a SQL Azure, en la **archivo** menú, seleccione **volver a conectarse a SQL Azure.**  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Conectarse a la base de datos de SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
