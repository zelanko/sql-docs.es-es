---
title: Conversión y las opciones de migración (AccessToSQL) | Microsoft Docs
ms.prod: sql
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
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 21cbf6f3a5dac0b77669b940bf27be26198a4456
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394770"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Conversión de la configuración y opciones de migración (AccessToSQL)
Para cada proyecto SSMA, puede establecer las opciones de nivel de proyecto. Estas opciones especifican cómo se convierten los objetos, cómo migrar los datos y cómo se asignan los tipos de datos de origen a tipos de datos de destino. Antes de convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure o migrar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
## <a name="configuration-options-and-modes"></a>Los modos y opciones de configuración  
SSMA tiene cuatro conjuntos de opciones de configuración y los cuatro modos para configurar estas opciones: de forma predeterminada, Optimistic, completa y personalizada. Se recomienda el modo predeterminado para la mayoría de los usuarios. Use el modo optimista para conversiones sencillas. Use el modo completo si desea ver todos los mensajes. En el modo personalizado, establezca las opciones.  
  
La configuración se describe en la sección "Referencia de la interfaz de usuario" de esta documentación. Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, consulte los temas siguientes:  
  
-   [Configuración del proyecto (conversión)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Configuración del proyecto (migración)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Configuración del proyecto (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configuración del proyecto (asignación de tipo)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Configuración del proyecto (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Configuración de opciones de proyecto  
En SSMA, puede configurar la configuración predeterminada para todos los proyectos. Estos valores se guardan en el archivo de configuración de SSMA y se aplican a cualquier nuevo proyecto que cree.  
  
**Para especificar las opciones de proyecto predeterminadas**  
  
1.  En el **herramientas** menú, seleccione **configuración de proyecto predeterminada**.  
  
2.  En el **configuración de proyecto predeterminada** cuadro de diálogo, realice una de las siguientes acciones:  
  
    -   Seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración **versión de destino de migración** lista desplegable, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Conversión o migración o SQL Azure**.  
  
        > [!NOTE]  
        > Opción de SQL Azure está disponible en el **General** pestaña sólo si el tipo de proyecto creado es SQL Azure.  
  
    -   Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** en el **modo** cuadro de lista desplegable.  
  
    -   Para especificar un modo personalizado, seleccione **personalizado** en el **modo** cuadro, seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o escriba el valor o una configuración nueva.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración del proyecto actual. Esta configuración se guarda en el archivo de proyecto actual.  
  
**Para personalizar la configuración para el proyecto actual**  
  
1.  En el **herramientas** menú, seleccione **configuración del proyecto**.  
  
2.  En el **configuración del proyecto** cuadro de diálogo, realice una de las siguientes acciones:  
  
    -   Para seleccionar un modo predefinido, seleccione **predeterminado**, **Optimistic**, o **completa** en el **modo** cuadro de lista desplegable.  
  
    -   Para especificar un modo personalizado, seleccione **personalizado** en el **modo** cuadro, seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o escriba el valor o una configuración nueva.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso en la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [tipos de datos de destino y origen de asignación](mapping-source-and-target-data-types-accesstosql.md)  
  
-   Para personalizar la asignación de las bases de datos de origen y destino, vea [bases de datos de destino y origen de asignación](mapping-source-and-target-databases-accesstosql.md)  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de Access en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
