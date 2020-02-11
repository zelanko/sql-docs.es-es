---
title: Configuración de las opciones de conversión y migración (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, setting options
- migration options
- modes
- options, conversion settings
- project settings
- schemas
ms.assetid: 0a7304df-2f35-4453-96ef-7ac83dea1167
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3e89cfd6768aeedd970889cbaea46bb3e1ceae4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051499"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Configuración de las opciones de conversión y migración (AccessToSQL)
Para cada proyecto de SSMA, puede establecer opciones de nivel de proyecto. Estas opciones especifican cómo se convierten los objetos, cómo se migran los datos y cómo se asignan los tipos de datos de origen a los tipos de datos de destino. Antes de convertir objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure o migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
## <a name="configuration-options-and-modes"></a>Opciones de configuración y modos  
SSMA tiene cuatro conjuntos de opciones de configuración y cuatro modos para configurar estas opciones: default, optimistic, Full y Custom. El modo predeterminado es el recomendado para la mayoría de los usuarios. Use el modo optimista para las conversiones simples. Use el modo completo si desea ver todos los mensajes. En el modo personalizado, se establecen las opciones.  
  
La configuración se describe en la sección "referencia de la interfaz de usuario" de esta documentación. Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, vea los temas siguientes:  
  
-   [Configuración del proyecto (conversión)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Configuración del proyecto (migración)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Configuración del proyecto (GUI)](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configuración del proyecto (asignación de tipo)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Configuración del proyecto (SQL Azure)](https://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Configuración de opciones de proyecto  
En SSMA, puede configurar los valores predeterminados para todos los proyectos. Estas opciones se guardan en el archivo de configuración de SSMA y se aplican a cualquier proyecto nuevo que cree.  
  
**Para establecer las opciones predeterminadas del proyecto**  
  
1.  En el menú **herramientas** , seleccione **configuración predeterminada del proyecto**.  
  
2.  En el cuadro de diálogo **configuración predeterminada del proyecto** , realice una de las acciones siguientes:  
  
    -   Seleccione el tipo de proyecto de migración para el que es necesario ver o cambiar la configuración en la lista desplegable de la **versión de destino** de la migración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **conversión o migración o SQL Azure**.  
  
        > [!NOTE]  
        > SQL Azure opción solo está disponible en la pestaña **General** si el tipo de proyecto creado es SQL Azure.  
  
    -   Para seleccionar un modo predefinido, seleccione **predeterminado**, **optimista**o **completo** en el cuadro desplegable **modo** .  
  
    -   Para especificar un modo personalizado, seleccione **personalizado** en el cuadro **modo** , seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o especifique el nuevo valor o valor.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
También puede personalizar la configuración del proyecto actual. Esta configuración se guarda en el archivo de proyecto actual.  
  
**Para personalizar la configuración del proyecto actual**  
  
1.  En el menú **herramientas** , seleccione **configuración del proyecto**.  
  
2.  En el cuadro de diálogo **configuración del proyecto** , realice una de las acciones siguientes:  
  
    -   Para seleccionar un modo predefinido, seleccione **predeterminado**, **optimista**o **completo** en el cuadro desplegable **modo** .  
  
    -   Para especificar un modo personalizado, seleccione **personalizado** en el cuadro **modo** , seleccione una opción en el panel izquierdo, haga clic en la configuración o el valor en el panel derecho y, a continuación, seleccione o especifique el nuevo valor o valor.  
  
3.  Haga clic en **Aceptar** para guardar la configuración.  
  
## <a name="next-steps"></a>Pasos siguientes  
El siguiente paso de la migración depende de las necesidades del proyecto:  
  
-   Para personalizar la asignación de los tipos de datos de origen y de destino, vea [asignar tipos de datos de origen y de destino](mapping-source-and-target-data-types-accesstosql.md) .  
  
-   Para personalizar la asignación de bases de datos de origen y de destino, consulte [asignación de bases de datos de origen y de destino](mapping-source-and-target-databases-accesstosql.md) .  
  
-   De lo contrario, puede convertir las definiciones de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de Access en o SQL Azure definiciones de objeto. Para obtener más información, vea [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md) .  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
