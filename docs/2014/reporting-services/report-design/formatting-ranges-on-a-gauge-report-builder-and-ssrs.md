---
title: Aplicar formato a los rangos de un medidor (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e893b005e074f50828b04525c1c1f963a801489e
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287343"
---
# <a name="formatting-ranges-on-a-gauge-report-builder-and-ssrs"></a>Aplicar formato a los rangos de un medidor (Generador de informes y SSRS)
  Un intervalo de medidor es una zona o área en la escala del medidor que indica una subsección importante de valores en el medidor. Use un intervalo de medidor para indicar visualmente el momento en el que el valor de puntero entra en cierto intervalo de valores. Los intervalos están definidos por un valor inicial y un valor final.  
  
 También se pueden usar intervalos para definir secciones diferentes de un medidor. Por ejemplo, en un medidor con valores comprendidos entre 0 y 10, puede definir un intervalo rojo para los valores comprendidos entre 0 y 3, un intervalo amarillo para los valores comprendidos entre 4 y 7 y un intervalo verde para los valores comprendidos entre 8 y 10. Si el valor inicial especificado es mayor que el valor final especificado, se intercambian los valores para que el valor inicial sea el valor final y el valor final sea el valor inicial.  
  
 Puede colocar el intervalo del mismo modo que coloca los punteros en una escala. Las propiedades **Posición** y **Distancia desde escala** determinan la posición del intervalo. Para obtener más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las escalas de un medidor &#40;Generador de informes y SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Establecer un valor mínimo o máximo en un medidor &#40;Generador de informes y SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un KPI a un informe &#40;generador de informes&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
