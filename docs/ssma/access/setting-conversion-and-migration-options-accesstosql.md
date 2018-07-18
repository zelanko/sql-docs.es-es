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
ms.openlocfilehash: bf73284de3f23aa861c446e4a2ed67278f4a5ce5
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979707"
---
# <a name="setting-conversion-and-migration-options-accesstosql"></a>Conversión de la configuración y opciones de migración (AccessToSQL)
Para cada proyecto SSMA, puede establecer las opciones de nivel de proyecto. Estas opciones especifican cómo se convierten los objetos, cómo migrar los datos y cómo se asignan los tipos de datos de origen a tipos de datos de destino. Antes de convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure o migrar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, compruebe que las opciones de configuración son adecuadas para el proyecto.  
  
## <a name="configuration-options-and-modes"></a>Los modos y opciones de configuración  
SSMA tiene cuatro conjuntos de opciones de configuración y los cuatro modos para configurar estas opciones: de forma predeterminada, Optimistic, completa y personalizada. Se recomienda el modo predeterminado para la mayoría de los usuarios. Use el modo optimista para conversiones sencillas. Use el modo completo si desea ver todos los mensajes. En el modo personalizado, establezca las opciones.  
  
La configuración se describe en la sección "Referencia de la interfaz de usuario" de esta documentación. Para obtener más información sobre la configuración y cómo se aplica la configuración en cada modo, consulte los temas siguientes:  
  
-   [Configuración del proyecto (conversión)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
-   [Configuración del proyecto (migración)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)  
  
-   [Configuración del proyecto (GUI)](http://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)  
  
-   [Configuración del proyecto (asignación de tipo)](http://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655)  
  
-   [Configuración del proyecto (SQL Azure)](http://msdn.microsoft.com/bbb8a204-d0e4-4f0b-9709-271feb1f136e)  
  
## <a name="setting-project-options"></a>Establecer las opciones de proyecto  
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
  
-   Para personalizar la asignación de tipos de datos de origen y destino, vea [tipos de datos de destino y origen de asignación](http://msdn.microsoft.com/b362a075-16e7-423f-b63f-e1e9f02844a9)  
  
-   Para personalizar la asignación de las bases de datos de origen y destino, vea [bases de datos de destino y origen de asignación](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
-   En caso contrario, puede convertir las definiciones de objeto de base de datos de Access en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o definiciones de objetos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
