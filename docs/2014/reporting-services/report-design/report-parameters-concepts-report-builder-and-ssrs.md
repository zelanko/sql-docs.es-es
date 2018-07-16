---
title: Notificar el concepto de parámetros (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 860099dc49e0fe383d7b53ac379c4671ead2477b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296065"
---
# <a name="report-parameters-concept-report-builder-and-ssrs"></a>Concepto de parámetros de informe (Generador de informes y SSRS)
  Puede agregar parámetros a un informe para vincular informes relacionados, controlar la apariencia del informe, filtrar datos del informe o restringir el ámbito del informe a usuarios o ubicaciones específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Los parámetros de informe se crean de las formas siguientes:  
  
-   Automáticamente, cuando se define una consulta de conjunto de datos que contiene variables de consulta. Para cada variable de consulta, se crean un parámetro de consulta de conjunto de datos y un parámetro de informe correspondientes con los mismos nombres. Un parámetro de consulta puede ser una referencia a una variable de consulta o a un parámetro de entrada para un procedimiento almacenado.  
  
-   Automáticamente, cuando se agrega una referencia a un conjunto de datos compartido que contiene parámetros de consulta.  
  
-   Manualmente, cuando se crean parámetros de informe en el panel Datos de informe. Los parámetros son una de las colecciones integradas que puede incluir en una expresión o informe. Dado que las expresiones se utilizan para definir valores a lo largo de una definición de informe, puede utilizar parámetros para controlar la apariencia del informe o para pasar valores a los subinformes relacionados o a los informes que también usan parámetros.  
  
 Para obtener más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md).  
  
 Los parámetros se utilizan con frecuencia para filtrar los datos del informe antes y después de que se devuelvan los datos al informe. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Cuando diseñe un informe, los parámetros de informe se guardarán en la definición de informe. Cuando diseñe un informe, los parámetros de informe se guardarán y administrarán por separado, no con la definición de informe. Después de guardar el informe en el servidor de informes, puede hacer lo siguiente:  
  
-   Cambiar directamente los valores de los parámetros de informe en el servidor de informes independientemente de la definición de informe.  
  
-   Crear varios informes vinculados en los que cada uno sea un vínculo a la definición de informe con un conjunto independiente de valores de parámetros que se pueden administrar de forma separada en el servidor de informes.  
  
 Si está pensando crear instantáneas de informe, historiales o suscripciones a un informe publicado, debe saber cómo afectan los parámetros de informe a los requisitos de diseño del informe.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de creación de informes &#40;generador de informes y SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro al informe &#40;generador de informes&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
