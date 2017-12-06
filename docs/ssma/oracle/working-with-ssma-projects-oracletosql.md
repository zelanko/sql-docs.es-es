---
title: Trabajar con proyectos SSMA (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: "11"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 3fbafb9a5357092aee293b9b190156d4bcca84d6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-ssma-projects-oracletosql"></a>Trabajar con proyectos SSMA (OracleToSQL)
Para migrar bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], primero cree un proyecto SSMA. El proyecto es un archivo que contiene la información siguiente:  
  
-   Metadatos acerca de las bases de datos de Oracle que van a migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Metadatos acerca de la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que recibirá los objetos migrados y los datos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]información de conexión.  
  
-   Configuración del proyecto.  
  
Cuando se abre un proyecto, se desconecta de Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que le permite trabajar sin conexión. Para obtener información acerca de cómo volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectarse a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de configuración de conversión y cargar objetos de base de datos, migración de datos y la sincronización de SSMA con Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Los valores predeterminados son adecuados para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debería revisar la configuración. Si desea, puede cambiar la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a los valores que se necesitan para puede ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revisar y cambiar la configuración según sea necesario. Para obtener más información acerca de estas opciones, consulte [configuración del proyecto &#40; Conversión &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Repita los pasos 1 a 3 para las páginas de la migración, la sincronización, cargar objetos del sistema, interfaz gráfica de usuario y asignación de tipo.  
  
    -   Para obtener información acerca de la configuración de la migración, consulte [configuración del proyecto &#40; Migración de &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración del objeto de sistema, consulte [configuración del proyecto &#40; Cargar objetos del sistema &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Para obtener información sobre la configuración de sincronización para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [configuración del proyecto &#40; Sincronización &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración de la interfaz gráfica de usuario, consulte [configuración del proyecto &#40; Interfaz gráfica de usuario &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto &#40; Asignación de tipos de &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Crear nuevos proyectos  
Para migrar datos de bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], primero debe crear un proyecto.  
  
**Para crear un proyecto**  
  
1.  En el **archivo** menú, haga clic en **nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** cuadro, escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto y, a continuación, haga clic en **Aceptar**.  
  
4.  En el **migración a** de lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Base de datos de SQL Azure  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto que se aplican a todos los nuevos proyectos SSMA, puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [definir opciones de proyecto &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Si desea personalizar asignaciones de tipos de datos entre las bases de datos de origen y de destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información, consulte [asignación de Oracle y tipos de datos de SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Guardar proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, haga clic en **Guardar proyecto**.  
  
    Si los esquemas del proyecto han cambiado o que no se ha convertido, SSMA le pedirá que para cargar y guardar los metadatos. Cargar y guardar los metadatos le permitirá trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, como el personal de soporte técnico. Si le pide que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada esquema que muestra un estado de **faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar los metadatos puede tardar varios minutos. Si no desea guardar los metadatos, no seleccione las casillas de verificación.  
  
    2.  Haga clic en el **guardar** botón.  
  
        SSMA analizará los esquemas de Oracle y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Cuando se abre un proyecto, se desconecta de Oracle y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Que le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para migrar datos, debe volver a conectarse a Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, haga clic en el proyecto que desea abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .o2ssproj, seleccione el archivo y, a continuación, haga clic en **abiertos**.  
  
2.  Para volver a conectarse a Oracle, en la **archivo** menú, haga clic en **volver a conectar con Oracle**.  
  
3.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], en la **archivo** menú, haga clic en **volver a conectar a SQL Server**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [conectarse a la base de datos de Oracle (OracleToSQL)](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Conectarse a la base de datos de Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Conectarse a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
