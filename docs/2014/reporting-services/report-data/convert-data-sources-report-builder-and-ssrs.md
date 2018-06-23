---
title: Convertir un origen de datos incrustado en compartido (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: 15
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 6a56cf7b9f2e087f44166f2ded7cb55ebf95b01c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111093"
---
# <a name="convert-a-data-source-from-embedded-to-shared-report-builder-and-ssrs"></a>Convertir un origen de datos incrustado en compartido (Generador de informes y SSRS)
  Cada origen de datos del panel Datos de informe está incrustado y es específico del informe, o está compartido. En el Generador de informes, un origen de datos compartido señala un origen de datos compartido publicado en un servidor de informes o un sitio de SharePoint. En el Diseñador de informes, un origen de datos compartido señala un origen de datos compartido de la carpeta **Orígenes de datos compartidos** en el Explorador de soluciones.  
  
 Para más información sobre las diferencias entre orígenes de datos insertados y compartidos, vea [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 Para más información sobre cómo crear un origen de datos compartido, vea [Crear un origen de datos incrustado o compartido &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Diseñador de informes  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para convertir un origen de datos incrustado en compartido  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos y, después, haga clic en **Convertir a origen de datos compartidos**.  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no está visible, haga clic en **Datos de informe** en el menú **Ver**. Si el panel se abre como una ventana flotante, puede acoplarlo. Para más información, vea [Acoplar el panel Datos de informe en el Diseñador de informes &#40;SSRS&#41;](../tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido. En el Explorador de soluciones, aparece un origen de datos compartido con el mismo nombre bajo la carpeta **Origen de datos compartido** .  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para convertir un origen de datos compartido en incrustado  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos, abra el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información requerida.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
## <a name="report-builder"></a>Generador de informes  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para convertir un origen de datos incrustado en compartido  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos para abrir el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información requerida.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para convertir un origen de datos compartido en incrustado  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos, abra el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información requerida.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
## <a name="see-also"></a>Vea también  
 [Administrar los orígenes de datos de informe](manage-report-data-sources.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  