---
title: Establecer las opciones de proyecto (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Setting project options,configuration options
ms.assetid: 08820d88-e157-4d49-9401-38580dd7ec2d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e397bf4480dd7a9955fb8c7acbce0d11fd910893
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663974"
---
# <a name="setting-project-options-mysqltosql"></a>Configuración de opciones de proyecto (MySQLToSQL)
Para cada proyecto SSMA, puede establecer las opciones de nivel de proyecto. Estas opciones especifican cómo se convierten los objetos, cómo migrar los datos y cómo se asignan los tipos de datos de origen a tipos de datos de destino.  Antes de convertir objetos de SQL Server o SQL Azure o migrar datos a SQL Server o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
SSMA le permite configurar las opciones predeterminadas para todos los proyectos. Estas opciones se aplican a cualquier nuevo proyecto que cree. A continuación, puede personalizar las opciones para cada proyecto.  
  
## <a name="configuration-options-and-modes"></a>Los modos y opciones de configuración  
SSMA tiene cinco conjuntos de configuración del proyecto:  
  
-   Información del proyecto  
  
-   General (conversión, migración y SQL Azure)  
  
-   Synchronization  
  
-   INTERFAZ GRÁFICA DE USUARIO  
  
-   Asignación de tipos  
  
La configuración del proyecto se puede configurar de cuatro maneras:  
  
-   Default  
  
-   Optimistic  
  
-   Completo  
  
-   Personalizado  
  
Se recomienda el modo predeterminado para la mayoría de los usuarios. El modo optimista mantiene más de la sintaxis actual de MySQL y es más fácil de leer. Sin embargo, mantener la sintaxis actual podría no ser precisa. Si la sintaxis de MySQL se debe convertir en sintaxis de SQL Server o SQL Azure equivalente, el modo completo realiza la conversión más completa. Sin embargo, el código resultante, podría ser más difícil de leer. En el modo personalizado, puede establecer las opciones.  
  
Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, consulte los temas siguientes:  
  
-   [Configuración del proyecto &#40;conversión&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
-   [Configuración del proyecto &#40;migración&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)  
  
-   [Configuración del proyecto (GUI) (SSMA común)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configuración del proyecto &#40;asignación de tipos de&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)  
  
-   [Configuración del proyecto &#40;sincronización&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
-   [Configuración del proyecto &#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)  
  
## <a name="setting-project-options"></a>Configuración de opciones de proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Estos valores se guardan en el archivo de configuración de SSMA y se aplican a cualquier nuevo proyecto que cree.  
  
**Para especificar las opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, haga clic en **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, use uno de los siguientes procedimientos:  
  
    1.  Seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración **versión de destino de migración** lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Conversión o migración o SQL Azure** opción.  
  
    2.  Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** desde el **modo** cuadro de lista desplegable.  
  
    3.  Para especificar una configuración personalizada, seleccione o escriba la nueva configuración o valores.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración para el proyecto actual. La configuración se guarda en el archivo de proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, haga clic en **ProjectSettings**.  
  
2.  En el **ProjectSettings** cuadro de diálogo, use uno de los siguientes procedimientos:  
  
    1.  Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** desde el **modo** cuadro de lista desplegable.  
  
    2.  Para especificar un modo personalizado, seleccione **personalizado** desde el **modo** cuadro de lista desplegable. Y, a continuación, seleccione la configuración de proyecto adecuada.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [asignación MySQL y tipos de datos de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de MySQL a SQL Server o las definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir las bases de datos de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Asignación de tipos de datos SQL Server y de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
