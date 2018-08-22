---
title: Trabajar con proyectos de SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 76dd1388f5abdc2219270f0745c03fcdb0334030
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393028"
---
# <a name="working-with-ssma-projects-oracletosql"></a>Proyectos de SSMA (OracleToSQL)
Para migrar bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], creará primero un proyecto de SSMA. El proyecto es un archivo que contiene la información siguiente:  
  
-   Metadatos acerca de las bases de datos de Oracle que van a migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Metadatos acerca de la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que recibirán los objetos migrados y los datos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de conexión.  
  
-   Configuración del proyecto.  
  
Al abrir un proyecto, se desconecta de Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Que le permite trabajar sin conexión. Para obtener información sobre cómo volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Revisar la configuración predeterminada del proyecto  
SSMA contiene varias opciones de conversión y cargar objetos de base de datos, migración de datos y sincronización SSMA con Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los valores predeterminados son adecuados para muchos usuarios. Sin embargo, antes de crear un nuevo proyecto SSMA, debe revisar la configuración. Si desea, puede cambiar la configuración predeterminada que se usará para todos los proyectos nuevos.  
  
**Para revisar la configuración predeterminada del proyecto**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  Seleccione el tipo de proyecto en **versión de destino de migración** a qué opciones de configuración son necesarios para ver o cambiar y, a continuación, haga clic en el menú desplegable **General** ficha.  
  
3.  En el panel izquierdo, haga clic en **conversión**.  
  
4.  En el panel derecho, revisar y cambiar la configuración según sea necesario. Para obtener más información sobre estas opciones, consulte [configuración del proyecto &#40;conversión&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Repita los pasos 1 a 3 para las páginas de la migración, sincronización, al cargar objetos del sistema, interfaz gráfica de usuario y asignación de tipos.  
  
    -   Para obtener información acerca de la configuración de la migración, consulte [configuración del proyecto &#40;migración&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración de objeto del sistema, consulte [configuración del proyecto&#40;cargar objetos del sistema&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Para obtener información sobre la configuración de sincronización a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [configuración del proyecto&#40;sincronización&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración de la interfaz gráfica de usuario, consulte [configuración del proyecto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Para obtener información acerca de la configuración de asignación de tipos de datos, vea [configuración del proyecto &#40;asignación de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Creación de nuevos proyectos  
Para migrar datos desde bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], primero debe crear un proyecto.  
  
**Para crear un proyecto**  
  
1.  En el **archivo** menú, haga clic en **nuevo proyecto**.  
  
    Aparecerá el cuadro de diálogo **Nuevo proyecto** .  
  
2.  En el **nombre** , escriba un nombre para el proyecto.  
  
3.  En el **ubicación** cuadro, escriba o seleccione una carpeta para el proyecto y, a continuación, haga clic en **Aceptar**.  
  
4.  En el **migración a** lista desplegable, seleccione la versión de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados para la migración. Las opciones disponibles son:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Base de datos SQL Azure  
  
## <a name="customizing-project-settings"></a>Personalizar la configuración de proyecto  
Además de definir la configuración predeterminada del proyecto que se aplica a todos los nuevos proyectos SSMA, puede personalizar la configuración para cada proyecto. Para obtener más información, consulte [definir opciones de proyecto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Al personalizar las asignaciones de tipos de datos entre bases de datos de origen y destino, puede definir asignaciones en el proyecto, la base de datos o el nivel de objeto. Para obtener más información, consulte [asignación de Oracle y SQL Server Data Types &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Guardando proyectos  
Cuando se guarda un proyecto, SSMA conserva la configuración del proyecto y, opcionalmente, los metadatos de la base de datos, en el archivo de proyecto.  
  
**Para guardar un proyecto**  
  
-   En el **archivo** menú, haga clic en **Guardar proyecto**.  
  
    Si los esquemas del proyecto han cambiado o no se han convertido, SSMA le pedirá que cargue y guarde los metadatos. Cargar y guardar los metadatos le permitirá trabajar sin conexión. También le permite enviar un archivo de proyecto completo a otras personas, como el personal de soporte técnico. Si se le pedirá que guarde los metadatos, realice lo siguiente:  
  
    1.  Para cada esquema que muestra el estado **donde faltan metadatos**, active la casilla situada junto al nombre de la base de datos.  
  
        Guardar metadatos podría tardar varios minutos. Si no desea guardar los metadatos aún, no seleccione las casillas de verificación.  
  
    2.  Haga clic en el **guardar** botón.  
  
        SSMA analizará los esquemas de Oracle y guardar los metadatos en el archivo de proyecto.  
  
## <a name="opening-projects"></a>Abrir proyectos  
Al abrir un proyecto, se desconecta de Oracle y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Que le permite trabajar sin conexión. Para actualizar los metadatos, cargar los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para migrar datos, debe volver a conectarse a Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para abrir un proyecto**  
  
1.  Realice uno de los siguientes procedimientos:  
  
    -   En el **archivo** menú, elija **proyectos recientes**y, a continuación, haga clic en el proyecto que desee abrir.  
  
    -   En el **archivo** menú, seleccione **Abrir proyecto**, busque el archivo de proyecto .o2ssproj, seleccione el archivo y, a continuación, haga clic en **abierto**.  
  
2.  Para volver a conectarse a Oracle, en la **archivo** menú, haga clic en **volver a conectar con Oracle**.  
  
3.  Para volver a conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el **archivo** menú, haga clic en **volver a conectar a SQL Server**.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración es [conectarse a la base de datos de Oracle (OracleToSQL)](http://msdn.microsoft.com/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Conexión a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
