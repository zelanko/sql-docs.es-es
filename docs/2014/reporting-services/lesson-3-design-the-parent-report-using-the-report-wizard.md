---
title: 'Lección 3: Diseñar el informe primario usando el Asistente para informes | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5cd312338aba04b3e70a18ca6fd71503b544e851
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036956"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>Lección 3: Diseñar el informe primario usando al Asistente para informes
  Después de crear una conexión de datos y una tabla de datos para el informe primario, el paso siguiente consiste en diseñar dicho informe usando el Asistente para informes del Diseñador de informes. Para más información sobre el Diseñador de informes, vea [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>Para diseñar el informe primario usando el Asistente para informes  
  
1.  Asegúrese de que el sitio web de nivel superior está seleccionado en el **Explorador de soluciones**.  
  
2.  Haga clic con el botón derecho en el sitio web y seleccione **Agregar nuevo elemento**.  
  
3.  En el **Agregar nuevo elemento** cuadro de diálogo, seleccione **Asistente para informes**, escriba un nombre para el archivo de informe y, a continuación, haga clic en **agregar**.  
  
     Así se inicia el Asistente para informes.  
  
4.  En el **las propiedades del conjunto de datos** página, en el **origen de datos** cuadro, seleccione el **DataSet1** que creó en [lección 2: Definir una conexión de datos y una tabla de datos para el informe primario](lesson-2-define-a-data-connection-and-data-table-for-parent-report.md).  
    El cuadro **Conjuntos de datos disponibles** se actualiza automáticamente con la **DataTable** que creó anteriormente.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Organizar campos** , haga lo siguiente:  
  
    1.  Arrastre **ProductID**, **Name**, **ProductNumber**, **SafetyStockLevel**y **ReorderLevel** desde **Campos disponibles** hasta el cuadro **Valores** .  
  
    2.  Haga clic en la flecha situada junto a **SUM (ProductID)**, **SUM (safetystocklevel)**, **SUM (ReorderLevel)** y desactive el **suma** selección.  
  
7.  Haga clic en **siguiente** dos veces y, a continuación, haga clic en **finalizar** para cerrar el **Asistente para informes**.  
  
     Ahora ha creado el archivo .rdlc. El archivo se abre en el Diseñador de informes. El Tablix que se diseñó se muestra en la superficie de diseño.  
  
8.  Guarde el archivo .rdlc.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha diseñado correctamente el informe primario usando el Asistente para informes. A continuación, creará una conexión de datos y una tabla de datos para el informe secundario.  
  
  
