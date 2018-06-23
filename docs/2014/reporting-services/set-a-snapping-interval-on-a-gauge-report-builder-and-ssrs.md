---
title: Establecer un intervalo de ajuste en un medidor (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4ce2f81ddb04c088c909e07f6d842f53c35b3974
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112888"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>Establecer un intervalo de ajuste en un medidor (Generador de informes y SSRS)
  Un intervalo de ajuste define el múltiplo al que se redondean los valores. De forma predeterminada, el medidor señala el valor exacto del campo que se ha especificado en el panel de datos. Sin embargo, puede redondear el valor exacto hacia arriba o hacia abajo para que el puntero se ajuste a un intervalo preestablecido. Por ejemplo, si el valor del medidor es de 34,2 y especifica un intervalo de ajuste de 5, el puntero del medidor señalará 3,5. Si el valor del medidor es de 31,2 y especifica un intervalo de ajuste de 5, el puntero del medidor señalará 30.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>Para establecer un intervalo de ajuste en un medidor  
  
1.  Haga clic en cualquier lugar en los números del medidor para resaltar la escala.  
  
2.  Abra el panel de propiedades.  
  
    > [!NOTE]  
    >  Si no ve el panel de propiedades, haga clic en el **vista** ficha y, a continuación, seleccione la **propiedades** casilla de verificación.  
  
3.  En el **punteros** propiedad, haga clic en el botón (…). Se abre el Editor de la colección de punteros.  
  
4.  Establecer el **SnappingEnabled** propiedad `True`.  
  
5.  Establecer el **SnappingInterval** en un valor que representa el intervalo de ajuste. El puntero se ajustará al múltiplo de redondeo más cercano al valor que ha especificado.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las escalas de un medidor &#40;Generador de informes y SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  