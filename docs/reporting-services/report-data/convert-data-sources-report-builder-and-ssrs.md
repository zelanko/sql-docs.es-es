---
title: Conversión de orígenes de datos (Generador de informes) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05aee467c3e69c115bedfa498a546a4e1664ba71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081751"
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>Conversión de orígenes de datos (Generador de informes y SSRS)
  Cada origen de datos del panel Datos de informe está incrustado y es específico del informe, o está compartido. En el Generador de informes, un origen de datos compartido señala un origen de datos compartido publicado en un servidor de informes o un sitio de SharePoint. En el Diseñador de informes, un origen de datos compartido señala un origen de datos compartido de la carpeta **Orígenes de datos compartidos** en el Explorador de soluciones.  
  
 Para más información sobre las diferencias entre orígenes de datos insertados y compartidos, vea [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56).  
  
 Para más información sobre cómo crear un origen de datos compartido, vea [Crear un origen de datos incrustado o compartido &#40;SSRS&#41;](https://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Diseñador de informes  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para convertir un origen de datos incrustado en compartido  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos y, después, haga clic en **Convertir a origen de datos compartidos**.  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no está visible, haga clic en **Datos de informe** en el menú **Ver**. Si el panel se abre como una ventana flotante, puede acoplarlo. Para más información, vea [Acoplar el panel Datos de informe en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido. En el Explorador de soluciones, aparece un origen de datos compartido con el mismo nombre bajo la carpeta **Origen de datos compartido** .  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para convertir un origen de datos compartido en incrustado  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos, abra el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información necesaria.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
## <a name="report-builder"></a>Generador de informes  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Para convertir un origen de datos incrustado en compartido  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos para abrir el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información necesaria.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Para convertir un origen de datos compartido en incrustado  
  
-   En el panel Datos de informe, haga clic con el botón derecho en el origen de datos, abra el cuadro de diálogo **Propiedades del origen de datos** y, después, haga clic en **Conexión incrustada**. Escriba la información necesaria.  
  
     En el panel Datos de informe, el icono de origen de datos cambia al icono de origen de datos compartido.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar orígenes de datos de informe](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
