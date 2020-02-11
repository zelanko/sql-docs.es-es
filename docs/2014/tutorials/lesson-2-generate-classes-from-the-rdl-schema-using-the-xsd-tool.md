---
title: 'Lección 2: generar clases a partir del esquema RDL con la herramienta XSD | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f5f74c6621d329885e9149fce9a37c7418d9c37b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62653756"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>Lección 2: Generar clases a partir del esquema RDL con la herramienta xsd
  Una vez creado el proyecto de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], el siguiente paso es recuperar una copia local del esquema de definición de informe y ejecutar la herramienta de definición de esquemas XML (Xsd.exe).  
  
### <a name="to-generate-the-rdl-classes"></a>Para generar clases RDL  
  
1.  Abra una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer (o un explorador Web equivalente) y vaya a la dirección URL siguiente:  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  Una vez abierto el esquema RDL en el explorador, vaya al menú **archivo** y seleccione **Guardar como**.  
  
3.  Vaya a la ubicación en la que creó el proyecto de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] y guarde el esquema con el nombre de archivo ReportDefinition.xsd.  
  
4.  Una vez guardado el archivo, abra una instancia del [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] símbolo del sistema. Para abrir una instancia del símbolo del sistema, haga clic en el menú Inicio, seleccione **todos los programas**, **Microsoft Visual Studio 2010**, seleccione **Visual Studio Tools** y haga clic en **símbolo del sistema de Visual Studio (2010)**.  
  
5.  Cambie la ruta actual por la ubicación en la que guardó el archivo ReportDefinition.xsd:  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  Genere el archivo ReportDefinition.cs que contiene las clases para el esquema RDL con el siguiente comando:  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     Para generar un archivo ReportDefinition.vb, utilice este comando:  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  Agregue ReportDefinition.xsd al proyecto. En el menú **proyecto** , haga clic en **Agregar elemento existente**. Busque la ubicación del archivo ReportDefinition. xsd, seleccione ReportDefinition. xsd y haga clic en **Agregar**.  
  
    > [!NOTE]  
    >  Después de agregar el archivo ReportDefinition. xsd al proyecto, observará en **Explorador de soluciones** que el archivo ReportDefinition.CS (. VB) no está allí. Para mostrar el archivo, haga clic el botón de expandir o contraer situado junto al archivo ReportDefinition.xsd.  
  
## <a name="next-lesson"></a>Lección siguiente  
 En la siguiente lección, escribirá código para cargar una definición de informe desde un servidor de informes usando las clases generadas con el esquema RDL. Vea [Lección 3: cargar una definición de informe desde el servidor de informes](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar informes con clases generadas a partir del esquema RDL &#40;tutorial de SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
