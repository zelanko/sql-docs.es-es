---
title: Combinar celdas en una región de datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97e9280512b75aebfccb93c0e11e5402136fa6f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105569"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Combinar celdas en una región de datos (Generador de informes y SSRS)
  Puede mezclar celdas en una región de datos para combinarlas, mejorar la apariencia de la región de datos o proporcionar etiquetas para los grupos de columnas y de filas.  
  
> [!NOTE]  
>  Las celdas solo se pueden mezclar dentro de cada área de una región de datos: esquina, encabezados de columna, definición de grupo (o encabezados de fila) y cuerpo. No puede mezclar celdas situadas fuera de los límites del área. Por ejemplo, no puede mezclar una celda situada en el área de esquina de la región de datos con una celda situada en el área de grupo de filas. Para obtener más información sobre las áreas de Tablix, vea [lists &#40;generador de informes and SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>Para mezclar celdas en una región de datos  
  
1.  En la región de datos de la superficie de diseño del informe, haga clic en la primera celda que desea mezclar. Mantenga presionado el botón primario del mouse y arrastre vertical u horizontalmente para seleccionar celdas adyacentes. Las celdas seleccionadas quedan resaltadas.  
  
2.  Haga clic con el botón derecho en las celdas seleccionadas y seleccione **Combinar celdas**. Las celdas seleccionadas se combinan en una celda única.  
  
3.  Repita los pasos 1 y 2 para mezclar otras celdas adyacentes en una región de datos.  
  
## <a name="see-also"></a>Consulte también  
 [&#40;de la región de datos Tablix Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Enumera &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
