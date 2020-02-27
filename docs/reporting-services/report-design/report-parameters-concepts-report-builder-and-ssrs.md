---
title: Conceptos de parámetros de informe (Generador de informes) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b0aa2159-4e49-4713-8824-5ef9a9edbc62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e5e7cafdce773969f9e6914a47534f88eb238a4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081066"
---
# <a name="report-parameters-concepts-report-builder-and-ssrs"></a>Conceptos de parámetros de informe (generador de informes y SSRS)
  Puede agregar parámetros a un informe para vincular informes relacionados, controlar la apariencia del informe, filtrar datos del informe o restringir el ámbito del informe a usuarios o ubicaciones específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Los parámetros de informe se crean de las formas siguientes:  
  
-   Automáticamente, cuando se define una consulta de conjunto de datos que contiene variables de consulta. Para cada variable de consulta, se crean un parámetro de consulta de conjunto de datos y un parámetro de informe correspondientes con los mismos nombres. Un parámetro de consulta puede ser una referencia a una variable de consulta o a un parámetro de entrada para un procedimiento almacenado.  
  
-   Automáticamente, cuando se agrega una referencia a un conjunto de datos compartido que contiene parámetros de consulta.  
  
-   Manualmente, cuando se crean parámetros de informe en el panel Datos de informe. Los parámetros son una de las colecciones integradas que puede incluir en una expresión o informe. Dado que las expresiones se utilizan para definir valores a lo largo de una definición de informe, puede utilizar parámetros para controlar la apariencia del informe o para pasar valores a los subinformes relacionados o a los informes que también usan parámetros.  
  
 Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Los parámetros se utilizan con frecuencia para filtrar los datos del informe antes y después de que se devuelvan los datos al informe. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Cuando diseñe un informe, los parámetros de informe se guardarán en la definición de informe. Cuando diseñe un informe, los parámetros de informe se guardarán y administrarán por separado, no con la definición de informe. Después de guardar el informe en el servidor de informes, puede hacer lo siguiente:  
  
-   Cambiar directamente los valores de los parámetros de informe en el servidor de informes independientemente de la definición de informe.  
  
-   Crear varios informes vinculados en los que cada uno sea un vínculo a la definición de informe con un conjunto independiente de valores de parámetros que se pueden administrar de forma separada en el servidor de informes.  
  
 Si está pensando crear instantáneas de informe, historiales o suscripciones a un informe publicado, debe saber cómo afectan los parámetros de informe a los requisitos de diseño del informe.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md) [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
  
