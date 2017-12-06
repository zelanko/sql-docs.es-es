---
title: Trabajar con proyectos SSMA (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ed20ad1986bd80694dc452876cdd72aba23af82
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-ssma-projects-db2tosql"></a>Trabajar con proyectos SSMA (DB2ToSQL)
Para migrar bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], primero cree un proyecto SSMA. El proyecto es un archivo que contiene la información siguiente:  
  
-   Metadatos acerca de las bases de datos de DB2 que van a migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Metadatos acerca de la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que recibirá los objetos migrados y los datos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]información de conexión.  
  
-   Configuración del proyecto.  
  
Cuando se abre un proyecto, se desconecta de DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que le permite trabajar sin conexión. Para obtener información acerca de cómo volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectarse a SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de configuración de conversión y cargar objetos de base de datos, migrar datos y sincronizar SSMA con DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Los valores predeterminados son adecuados para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debería revisar la configuración. Si desea, puede cambiar la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a los valores que se necesitan para puede ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revisar y cambiar la configuración según sea necesario. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto &#40; Conversión &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
5.  Repita los pasos 1 a 3 para las páginas de la migración, la sincronización, cargar objetos del sistema, interfaz gráfica de usuario y asignación de tipo.  
  
    -   Para obtener información acerca de la configuración de la migración, consulte [configuración del proyecto &#40; Migración de &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-migration-db2tosql.md).  
  
    -   Para obtener información acerca de la configuración del objeto de sistema, consulte [configuración del proyecto &#40; Cargar objetos del sistema &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md).  
  
    -   Para obtener información sobre la configuración de sincronización para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [configuración del proyecto &#40; Sincronización &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
    -   Para obtener información acerca de la configuración de la interfaz gráfica de usuario, consulte [configuración del proyecto &#40; Interfaz gráfica de usuario &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-gui-db2tosql.md).  
  
    -   Para obtener información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto &#40; Asignación de tipos de &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="creating-new-projects"></a>Crear nuevos proyectos  
Para migrar datos de bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], primero debe crear un proyecto.  
  
**Para crear un proyecto**  
  
1.  En el **archivo** menú, haga clic en **nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto y, a continuación, haga clic en **Aceptar**.  
  
4.  En el **migración a** de lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Base de datos de SQL Azure  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto que se aplican a todos los nuevos proyectos SSMA, puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [definir opciones de proyecto &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md) y secciones relacionadas.  
  
Si desea personalizar asignaciones de tipos de datos entre las bases de datos de origen y de destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información, consulte [asignación DB2 y tipos de datos de SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
## <a name="saving-projects"></a>Guardar proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, haga clic en **Guardar proyecto**.  
  
    Si los esquemas del proyecto han cambiado o que no se ha convertido, SSMA le pedirá que para cargar y guardar los metadatos. Cargar y guardar los metadatos le permitirá trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, como el personal de soporte técnico. Si le pide que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada esquema que muestra un estado de **faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar los metadatos puede tardar varios minutos. Si no desea guardar los metadatos, no seleccione las casillas de verificación.  
  
    2.  Haga clic en el **guardar** botón.  
  
        SSMA analizará los esquemas de DB2 y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Cuando se abre un proyecto, se desconecta de DB2 y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para migrar datos, debe volver a conectar a DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, haga clic en el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .o2ssproj, seleccione el archivo y, a continuación, haga clic en **abiertos**.  
  
2.  Para volver a conectar a DB2, en la **archivo** menú, haga clic en **volver a conectar a DB2**.  
  
3.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], en la **archivo** menú, haga clic en **volver a conectar a SQL Server**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [conectarse a la base de datos DB2](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[Conectarse a la base de datos DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[Conectarse a SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
