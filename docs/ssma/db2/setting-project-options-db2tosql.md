---
title: Establecer las opciones de proyecto (DB2ToSQL) | Documentos de Microsoft
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
ms.assetid: f325a606-97ac-48bc-b344-b55f5e086a48
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1f5b71db23d56150fbc6a2f7990ba9960d83d2d1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-db2tosql"></a>Establecer las opciones del proyecto (DB2ToSQL)
Para cada proyecto SSMA puede establecer opciones de nivel de proyecto. Estas opciones especifican la conversión de objetos, la carga del objeto, la configuración de migración de datos y la interfaz de usuario. Antes de convertir objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o migrar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
SSMA le permite configurar las opciones predeterminadas para todos los proyectos. Estas opciones se aplican a cualquier proyecto nuevo que cree. A continuación, puede personalizar las opciones para cada proyecto.  
  
## <a name="configuration-options-and-modes"></a>Modos y opciones de configuración  
SSMA tiene cinco conjuntos de configuración del proyecto:  
  
-   Información del proyecto  
  
-   General (conversión y migración, cargar objetos)  
  
-   Synchronization  
  
-   INTERFAZ GRÁFICA DE USUARIO  
  
-   Asignación de tipos  
  
También tiene cuatro modos para configurar estas opciones:  
  
-   Predeterminado  
  
-   Optimistic  
  
-   Completa  
  
-   Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis de DB2 actual y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser exactos. Si se debe convertir la sintaxis de DB2 a equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis, el modo completo realiza la conversión más completa, pero el código resultante podría ser más difícil de leer. En el modo personalizado, establezca las opciones.  
  
Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, vea los temas siguientes:  
  
-   [Configuración del proyecto &#40; Conversión &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)  
  
-   [Configuración del proyecto &#40; Migración de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-migration-db2tosql.md)  
  
-   [Configuración del proyecto &#40; Sincronización &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)  
  
-   [Configuración del proyecto &#40; Interfaz gráfica de usuario &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-gui-db2tosql.md)  
  
-   [Configuración del proyecto &#40; Asignación de tipos de &#41; &#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)  
  
## <a name="setting-project-options"></a>Establecer las opciones del proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Esta configuración se guarda en el archivo de configuración de SSMA y aplicarse a un proyecto nuevo que cree.  
  
**Para establecer opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    -   Seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** desplegable haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione conversión o migración.  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completo**.  
  
    -   Para especificar una configuración personalizada, seleccione o escriba la nueva configuración o valores.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración del proyecto actual. Esta configuración se guarda en el archivo del proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, haga clic en **configuración del proyecto**.  
  
2.  En el **configuración del proyecto** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    -   Para seleccionar un modo predefinido, en el **modo** cuadro de lista desplegable, seleccione **predeterminado**, **Optimistic**, o **completo**.  
  
    -   Para especificar un modo personalizado, en el **modo** cuadro, seleccione **personalizado**y, a continuación, seleccione la configuración de proyecto adecuada.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [DB2 de asignación y tipos de datos de SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiciones de objetos. Para obtener más información, consulte [convertir esquemas de DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Vea también  
[Asignación de DB2 y tipos de datos SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)  
  

