---
title: Establecer las opciones de proyecto (MySQLToSQL) | Documentos de Microsoft
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
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 005889e4a4fc813819f6133d7a5a7b2a5223b861
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="setting-project-options-mysqltosql"></a>Establecer las opciones del proyecto (MySQLToSQL)
Para cada proyecto SSMA, puede establecer opciones de nivel de proyecto. Estas opciones especifican cómo se convierten los objetos, cómo se migran los datos y cómo se asignan los tipos de datos de origen a tipos de datos de destino.  Antes de convertir los objetos a SQL Server o SQL Azure o migrar datos a SQL Server o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
SSMA le permite configurar las opciones predeterminadas para todos los proyectos. Estas opciones se aplican a cualquier proyecto nuevo que cree. A continuación, puede personalizar las opciones para cada proyecto.  
  
## <a name="configuration-options-and-modes"></a>Modos y opciones de configuración  
SSMA tiene cinco conjuntos de configuración del proyecto:  
  
-   Información del proyecto  
  
-   General (conversión, migración y SQL Azure)  
  
-   Synchronization  
  
-   INTERFAZ GRÁFICA DE USUARIO  
  
-   Asignación de tipos  
  
La configuración del proyecto puede configurarse de cuatro maneras:  
  
-   Predeterminado  
  
-   Optimistic  
  
-   Completa  
  
-   Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis de MySQL actual y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser exactos. Si la sintaxis de MySQL deben convertirse en sintaxis de SQL Server o SQL Azure equivalente, el modo completo realiza la conversión más completa. Sin embargo, el código resultante, sería más difícil de leer. En el modo personalizado, puede establecer las opciones.  
  
Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, vea los temas siguientes:  
  
-   [Configuración del proyecto &#40; Conversión &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Configuración del proyecto &#40; Migración de &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Configuración del proyecto (GUI) (SSMA común)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configuración del proyecto &#40; Asignación de tipos de &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Configuración del proyecto &#40; Sincronización &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Configuración del proyecto &#40; Base de datos de SQL Azure &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Establecer las opciones del proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Esta configuración se guarda en el archivo de configuración de SSMA y aplicarse a un proyecto nuevo que cree.  
  
**Para establecer opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    1.  Seleccione el tipo de proyecto de migración para el que se requiere para ver / cambiar de configuración **versión de destino de migración** de lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **conversión o migración o SQL Azure** opción.  
  
    2.  Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** desde el **modo** cuadro de lista desplegable.  
  
    3.  Para especificar una configuración personalizada, seleccione o escriba la nueva configuración o valores.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración para el proyecto actual. La configuración se guarda en el archivo del proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, haga clic en **ProjectSettings**.  
  
2.  En el **ProjectSettings** cuadro de diálogo, use uno de los procedimientos siguientes:  
  
    1.  Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** desde el **modo** cuadro de lista desplegable.  
  
    2.  Para especificar un modo personalizado, seleccione **personalizado** desde el **modo** cuadro de lista desplegable. Y, a continuación, seleccione la configuración de proyecto adecuada.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación de tipos de datos de origen y de destino, vea [MySQL de asignación y tipos de datos de SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de MySQL a SQL Server o definiciones de objetos de SQL Azure. Para obtener más información, vea [convertir bases de datos de MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Asignación de MySQL y tipos de datos SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  

