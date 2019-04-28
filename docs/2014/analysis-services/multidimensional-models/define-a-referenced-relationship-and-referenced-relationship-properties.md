---
title: Definir relaciones referenciadas y propiedades de las relaciones referenciadas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b173aa62dfe5656bfc784c766791c294453596c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700092"
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
  
  
