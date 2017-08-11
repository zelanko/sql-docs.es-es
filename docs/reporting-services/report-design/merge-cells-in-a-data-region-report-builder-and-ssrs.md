---
title: "Combinar celdas en una región de datos (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c643b94c86109a99e1448093b4b9744924fcd7f7
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Combinar celdas en una región de datos (Generador de informes y SSRS)
En un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , puede mezclar celdas en una región de datos para combinarlas, mejorar la apariencia de la región de datos o proporcionar etiquetas para los grupos de columnas y de filas.  
  
Solo puede combinar celdas dentro de cada área de una región de datos: esquina, encabezados de columna, definición de grupo (o encabezados de fila) y cuerpo. No puede combinar celdas situadas fuera de los límites del área. Por ejemplo, no puede combinar una celda situada en el área de esquina de la región de datos con una celda situada en el área de grupo de filas. Obtenga más información sobre [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-merge-cells-in-a-data-region"></a>Para mezclar celdas en una región de datos  
  
1.  En la región de datos de la superficie de diseño del informe, haga clic en la primera celda que desea mezclar. Mantenga presionado el botón primario del mouse y arrastre vertical u horizontalmente para seleccionar celdas adyacentes. Las celdas seleccionadas quedan resaltadas.  
  
2.  Haga clic con el botón derecho en las celdas seleccionadas y seleccione **Combinar celdas**. Las celdas seleccionadas se combinan en una celda única.  
  
3.  Repita los pasos 1 y 2 para mezclar otras celdas adyacentes en una región de datos.  
  
## <a name="see-also"></a>Vea también  
[Región de datos Tablix](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 [Tablas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Crear una matriz](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Creación de facturas y formularios con listas](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
[Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
