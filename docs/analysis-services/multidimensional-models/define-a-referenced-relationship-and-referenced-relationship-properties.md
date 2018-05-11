---
title: Definir relaciones referenciadas y propiedades de las relaciones referenciadas | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 89e3536c318d0c0fbf649beabe1aad6d90d7da49
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="define-a-referenced-relationship-and-referenced-relationship-properties"></a>Definir relaciones referenciadas y propiedades de las relaciones referenciadas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una relación de dimensión de referencia se define en la pestaña **Uso de dimensiones** del Diseñador de cubos. La relación de dimensión de referencia se define al especificar lo siguiente:  
  
-   La dimensión intermedia con la que se va a combinar. Puede ser una dimensión normal u otra dimensión de referencia.  
  
-   Un atributo de dimensión de referencia que defina el nivel mínimo en el que la dimensión está disponible para la agregación con respecto al grupo de medida.  
  
-   El atributo (clave externa) de la dimensión intermedia que corresponde al atributo de dimensión de referencia.  
  
 Tenga en cuenta que la columna que vincula la dimensión de referencia con la tabla de hechos, que suele ser el atributo clave de la dimensión de referencia, también debe ser definida como un atributo en la dimensión intermedia. Cuando cree una cadena de dimensiones de referencia, comience por crear la relación normal entre la primera dimensión de la cadena y el grupo de medida. A continuación, cree cada relación referenciada adicional en orden. Una relación referenciada solo se puede realizar para una dimensión que tenga una relación existente con el grupo de medida.  
  
 Cuando se crea una relación de dimensión de referencia, el vínculo del atributo de dimensión se materializa de forma predeterminada. El materializar un vínculo del atributo de dimensión hace que, durante el procesamiento, el valor del vínculo entre la tabla de hechos y la dimensión de referencia de cada fila se materialice, o almacene, en la estructura MOLAP de la dimensión. Esto tendrá un efecto poco importante en el rendimiento del proceso y en los requisitos de almacenamiento, pero mejorará el rendimiento de la consulta.  
  
 En una dimensión de referencia, la granularidad se especifica mediante la identificación del atributo que define la relación entre una dimensión de referencia y el grupo de medida correspondiente a la tabla principal de la dimensión. Cuando se encadenan varias dimensiones de referencia, las referencias definen la relación de la dimensión más externa al grupo de medida.  
  
  
