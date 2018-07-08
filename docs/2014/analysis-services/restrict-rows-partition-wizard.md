---
title: Restringir filas (Asistente para particiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b633b19331c836878487920e8145f12aae86f73
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167586"
---
# <a name="restrict-rows-partition-wizard"></a>Restringir filas (Asistente para particiones)
  Utilice la página **Restringir filas** para restringir las filas que se recuperarán de la tabla especificada y que se agregarán e incluirán en la partición.  
  
> [!NOTE]  
>  Esta página solo aparece si se ha seleccionado una única tabla en la página **Especificar información de origen** .  
  
> [!CAUTION]  
>  Si, en **Tablas disponibles** en la página **Especificar información de origen** , ha especificado una tabla que se usa en otra partición, debe proporcionar una consulta en la página **Restringir filas** ; de lo contrario, corre el riesgo de duplicar datos en el cubo.  
  
## <a name="options"></a>Opciones  
 **Especifique una consulta para restringir las filas**  
 Seleccione esta opción para escribir una consulta que restrinja las filas del cuadro **Consulta** .  
  
 Si la opción **Consulta** está vacía cuando se selecciona esta opción, dicha opción se rellena con una instrucción SQL que recupera todas las columnas y todas las filas de la tabla seleccionada con anterioridad.  
  
 **Consulta**  
 Escriba o modifique la instrucción SQL que se utiliza al recuperar filas de la tabla cuando se procesa la partición.  
  
> [!IMPORTANT]  
>  Si se especifica una cláusula WHERE, puede utilizarse un subconjunto de registros para esta partición. Esto es muy importante para evitar la duplicación de datos cuando varias particiones se basan en una única tabla de hechos.  
  
 **Comprobación**  
 Comprueba si la instrucción de **Consulta** es una instrucción SQL válida.  
  
## <a name="see-also"></a>Vea también  
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
