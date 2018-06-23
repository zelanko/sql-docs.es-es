---
title: Combinar celdas en una región de datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 31dcb2ef4f2d4881bd2e4ffb94865c9a9d71faad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201964"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Combinar celdas en una región de datos (Generador de informes y SSRS)
  Puede mezclar celdas en una región de datos para combinarlas, mejorar la apariencia de la región de datos o proporcionar etiquetas para los grupos de columnas y de filas.  
  
> [!NOTE]  
>  Las celdas solo se pueden mezclar dentro de cada área de una región de datos: esquina, encabezados de columna, definición de grupo (o encabezados de fila) y cuerpo. No puede mezclar celdas situadas fuera de los límites del área. Por ejemplo, no puede mezclar una celda situada en el área de esquina de la región de datos con una celda situada en el área de grupo de filas. Para obtener más información acerca de las áreas de tablix, vea [enumera &#40;el generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>Para mezclar celdas en una región de datos  
  
1.  En la región de datos de la superficie de diseño del informe, haga clic en la primera celda que desea mezclar. Mantenga presionado el botón primario del mouse y arrastre vertical u horizontalmente para seleccionar celdas adyacentes. Las celdas seleccionadas quedan resaltadas.  
  
2.  Haga clic con el botón derecho en las celdas seleccionadas y seleccione **Combinar celdas**. Las celdas seleccionadas se combinan en una celda única.  
  
3.  Repita los pasos 1 y 2 para mezclar otras celdas adyacentes en una región de datos.  
  
## <a name="see-also"></a>Vea también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  