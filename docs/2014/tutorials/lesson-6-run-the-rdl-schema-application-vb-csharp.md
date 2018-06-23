---
title: 'Lección 6: Ejecutar la aplicación del esquema RDL (VB-C#) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2cd2386-2df8-4b69-ab81-9ad1a31f6d27
caps.latest.revision: 15
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 95ef194a66d6c5480f8a83cbd0b78547e79804e6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201497"
---
# <a name="lesson-6-run-the-rdl-schema-application-vb-c"></a>Lección 6: Ejecutar la aplicación del esquema RDL (VB-C#)
  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ofrece dos métodos para generar y ejecutar una aplicación de consola desde el entorno de desarrollo integrado (IDE):  
  
-   Iniciar (con depuración)  
  
-   Iniciar sin depuración  
  
### <a name="to-build-and-run-the-samplerdlschema-application"></a>Para generar y ejecutar la aplicación SampleRDLSchema  
  
1.  En el menú **Depurar** , haga clic en **Iniciar sin depurar**. Esto garantiza que la ventana de la consola seguirá abierta cuando el programa se haya acabado de ejecutar.  
  
     La aplicación escribe lo siguiente en la consola:  
  
    ```  
    Loading Report Definition  
    Updating Report Definition  
    - Old Description: <Old Report Description>  
    - New Description: <New Report Description>  
    Publishing Report Definition  
    ```  
  
2.  Presione cualquier tecla para cerrar la consola.  
  
    > [!NOTE]  
    >  Los errores que se produzcan se escribirán en la consola.  
  
3.  Cuando la aplicación de ejemplo finaliza la ejecución de una copia actualizada del informe, la guarda en el servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar informes con clases generadas a partir del esquema RDL &#40;Tutorial de SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Report Definition Language &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  