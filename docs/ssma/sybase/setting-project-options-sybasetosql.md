---
title: Establecer las opciones de proyecto (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57954b06479e041772200fbb05ba823607a02ad5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="setting-project-options-sybasetosql"></a>Establecer las opciones del proyecto (SybaseToSQL)
Para cada proyecto SSMA, puede establecer opciones de nivel de proyecto. Estas opciones especifican la conversión de objetos, la carga del objeto, SQL azure, interfaz de usuario y configuración de la migración de datos. Antes de convertir objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure o migrar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
SSMA le permite configurar las opciones predeterminadas para todos los proyectos. Estas opciones se aplican a cualquier proyecto nuevo que cree. A continuación, puede personalizar las opciones para cada proyecto.  
  
## <a name="configuration-options-and-modes"></a>Modos y opciones de configuración  
SSMA tiene cinco conjuntos de configuración del proyecto:  
  
1.  Información del proyecto  
  
2.  General (conversión, migración y recopilación de datos)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  Asignación de tipos  
  
También tiene cuatro modos para configurar estas opciones:  
  
1.  Predeterminado  
  
2.  Optimistic  
  
3.  Completa  
  
4.  Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis de Sybase Adaptive Server Enterprise (ASE) actual y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser exactos. Si la sintaxis de ASE deben convertirse en equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o sintaxis de SQL Azure, el modo completo realiza una conversión completa, pero el código resultante podría ser más difícil de leer. En el modo personalizado, establezca las opciones.  
  
La configuración se describe en la sección de referencia de la interfaz de usuario de esta documentación. Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, vea los temas siguientes:  
  
-   [Configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;migración&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;sincronización&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;la asignación de tipo&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;base de datos de SQL Azure &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Establecer las opciones del proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Esta configuración se guarda en el archivo de configuración de SSMA y aplicarse a un proyecto nuevo que cree.  
  
**Para establecer opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    -   Seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** drop hacia abajo en General en la parte inferior del panel izquierdo y, a continuación, seleccione conversión o migración o SQL Azure.  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completo**.  
  
    -   Para especificar una configuración personalizada, seleccione o escriba la nueva configuración o los valores.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración del proyecto actual. Esta configuración se guarda en el archivo del proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
2.  En el **configuración del proyecto** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completo**.  
  
    -   Para especificar un modo personalizado, en el **modo** lista desplegable, seleccione **personalizado**, seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o escriba el valor o una configuración nueva.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Si quiere personalizado a la asignación de tipos de datos de origen y de destino, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de Sybase a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
