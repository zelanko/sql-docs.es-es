---
title: 'Lección 2: Generar clases a partir del esquema RDL con la herramienta xsd | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 67cbc84882683fcb31d6b42f69274d5166556450
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203542"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>Lección 2: Generar clases a partir del esquema RDL con la herramienta xsd
  Una vez creado el proyecto de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], el siguiente paso es recuperar una copia local del esquema de definición de informe y ejecutar la herramienta de definición de esquemas XML (Xsd.exe).  
  
### <a name="to-generate-the-rdl-classes"></a>Para generar clases RDL  
  
1.  Abra una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer (u otro explorador Web) y vaya a la dirección URL siguiente:  
  
    ```  
    http://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  Una vez se ha abierto el esquema RDL en el explorador, vaya a la **archivo** menú y seleccione **Guardar como**.  
  
3.  Vaya a la ubicación en la que creó el proyecto de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] y guarde el esquema con el nombre de archivo ReportDefinition.xsd.  
  
4.  Una vez guardado el archivo, abra una instancia de la [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] símbolo del sistema. Para abrir una instancia de la línea de comandos, haga clic en el menú Inicio, seleccione **todos los programas**, seleccione **Microsoft Visual Studio 2010**, seleccione **Visual Studio Tools** y haga clic en **Símbolo de visual Studio (2010)**.  
  
5.  Cambie la ruta actual por la ubicación en la que guardó el archivo ReportDefinition.xsd:  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  Genere el archivo ReportDefinition.cs que contiene las clases para el esquema RDL con el siguiente comando:  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     Para generar un archivo ReportDefinition.vb, utilice este comando:  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  Agregue ReportDefinition.xsd al proyecto. Desde el **proyecto** menú, haga clic en **Agregar elemento existente**. Vaya a la ubicación del archivo ReportDefinition.xsd, seleccione ReportDefinition.xsd y haga clic en **agregar**.  
  
    > [!NOTE]  
    >  Después de haber agregado el archivo ReportDefinition.xsd al proyecto, observará en **el Explorador de soluciones** que el archivo ReportDefinition.cs (.vb) no la encuentra. Para mostrar el archivo, haga clic el botón de expandir o contraer situado junto al archivo ReportDefinition.xsd.  
  
## <a name="next-lesson"></a>Lección siguiente  
 En la siguiente lección, escribirá código para cargar una definición de informe desde un servidor de informes usando las clases generadas con el esquema RDL. Vea [lección 3: cargar una definición de informe desde el servidor de informes](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Actualizar informes con clases generadas a partir del esquema RDL &#40;Tutorial de SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Report Definition Language &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  