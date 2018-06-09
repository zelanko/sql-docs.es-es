---
title: Establecer las opciones de proyecto (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 5c606de3c03038f7e2fbb9f974ba96dd64bef779
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777981"
---
# <a name="setting-project-options-oracletosql"></a>Establecer las opciones del proyecto (OracleToSQL)
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
  
-   Valor predeterminado  
  
-   Optimistic  
  
-   Completo  
  
-   Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis de Oracle actual y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser exactos. Si se debe convertir la sintaxis de Oracle a equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis, el modo completo realiza la conversión más completa, pero el código resultante podría ser más difícil de leer. En el modo personalizado, establezca las opciones.  
  
Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, vea los temas siguientes:  
  
-   [Configuración del proyecto &#40;conversión&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Configuración del proyecto &#40;migración&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [Configuración del proyecto&#40;sincronización&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Configuración del proyecto &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [Configuración del proyecto &#40;la asignación de tipo&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
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
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [asignación Oracle y tipos de datos de SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiciones de objetos. Para obtener más información, consulte [convertir esquemas de Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Asignación de Oracle y tipos de datos SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
