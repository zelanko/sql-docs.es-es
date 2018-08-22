---
title: Establecer las opciones de proyecto (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 9048eb69fd10cafc97daa91b5cac8571a4240cd0
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396345"
---
# <a name="setting-project-options-sybasetosql"></a>Configuración de opciones de proyecto (SybaseToSQL)
Para cada proyecto SSMA, puede establecer opciones de nivel de proyecto. Estas opciones especifican la conversión de objetos, la carga del objeto, SQL azure, interfaz de usuario y configuración de migración de datos. Antes de convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure o migrar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
SSMA le permite configurar las opciones predeterminadas para todos los proyectos. Estas opciones se aplican a cualquier nuevo proyecto que cree. A continuación, puede personalizar las opciones para cada proyecto.  
  
## <a name="configuration-options-and-modes"></a>Los modos y opciones de configuración  
SSMA tiene cinco conjuntos de configuración del proyecto:  
  
1.  Información del proyecto  
  
2.  General (conversión, migración y recopilación de datos)  
  
3.  Synchronization  
  
4.  INTERFAZ GRÁFICA DE USUARIO  
  
5.  Asignación de tipos  
  
También tiene cuatro modos para configurar estas opciones:  
  
1.  Default  
  
2.  Optimistic  
  
3.  Completo  
  
4.  Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis de Sybase Adaptive Server Enterprise (ASE) actual y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser precisa. Si se debe convertir la sintaxis de ASE a equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintaxis de SQL Azure, el modo completo realiza una conversión completa, pero el código resultante podría ser más difícil de leer. En el modo personalizado, establezca las opciones.  
  
La configuración se describe en la sección de referencia de la interfaz de usuario de esta documentación. Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, consulte los temas siguientes:  
  
-   [Configuración del proyecto &#40;conversión&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;migración&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;sincronización&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;asignación de tipos de&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Configuración del proyecto &#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Configuración de opciones de proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Estos valores se guardan en el archivo de configuración de SSMA y se aplican a cualquier nuevo proyecto que cree.  
  
**Para especificar las opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, use uno de los siguientes procedimientos:  
  
    -   Seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración **versión de destino de migración** drop hacia abajo, haga clic en General en la parte inferior del panel izquierdo y, a continuación, seleccione la conversión o la migración o SQL Azure.  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completa**.  
  
    -   Para especificar una configuración personalizada, seleccione o escriba la nueva configuración o valores.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración del proyecto actual. Esta configuración se guarda en el archivo de proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
2.  En el **configuración del proyecto** cuadro de diálogo, use uno de los siguientes procedimientos:  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completa**.  
  
    -   Para especificar un modo personalizado, en el **modo** lista desplegable, seleccione **personalizado**, seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o escriba el valor o una configuración nueva.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Si desea personalizado a la asignación de tipos de datos de origen y destino, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos Sybase en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
