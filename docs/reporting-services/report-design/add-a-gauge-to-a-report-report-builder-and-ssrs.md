---
title: Agregar un medidor a un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: daa8df71bddda27f42cc38e7f6b609208091a930
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>Agregar un medidor a un informe (Generador de informes y SSRS)
  En un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , cuando quiera resumir datos y presentarlos con un formato visual, puede usar una región de datos del medidor. Después de agregar una región de datos del medidor a la superficie de diseño, puede arrastrar los campos de conjunto de datos de informe a un panel de datos del medidor.  
  
## <a name="to-add-a-gauge-to-your-report"></a>Para agregar un medidor a un informe  
  
1.  Cree un informe o abra un informe existente.  
  
2.  En la pestaña Insertar, haga doble clic en Medidor. Se abre el cuadro de diálogo **Seleccionar tipo de medidor** .  
  
3.  Seleccione el tipo de medidor que desea agregar. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A diferencia de los gráficos, los medidores tienen solo dos tipos: lineales y radiales. Los medidores disponibles en el cuadro de diálogo **Seleccionar tipo de medidor** son plantillas para estos dos tipos de medidores. Por esta razón, no puede cambiar el tipo de medidor después de agregar el medidor a su informe. Para cambiar el tipo de un medidor, debe eliminarlo y volver a agregarlo.  
  
     Si el informe no tiene origen de datos y conjunto de datos, se abre el cuadro de diálogo **Propiedades del origen de datos** , que le guía en los pasos necesarios para crear ambos. Para más información, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
     Si el informe tiene un origen de datos, pero no un conjunto de datos, se abre el cuadro de diálogo **Propiedades del conjunto de datos** , que le guía en los pasos necesarios para crear uno. Para obtener más información, vea [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
4.  Haga clic en el medidor para mostrar el panel de datos. De forma predeterminada, un medidor tiene un puntero que corresponde a un valor. Puede agregar punteros adicionales.  
  
5.  Agregue un campo del conjunto de datos a la zona de colocación de campos de datos. Puede agregar solo un campo. Si desea mostrar varios, debe agregar punteros adicionales, uno para cada campo.  
  
     Haga doble clic en la escala del medidor y seleccione **Propiedades de escala**. Especifique los valores **Mínimo** y **Máximo** de la escala. Para más información, vea [Establecer un valor mínimo o máximo en un medidor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Anidar regiones de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
