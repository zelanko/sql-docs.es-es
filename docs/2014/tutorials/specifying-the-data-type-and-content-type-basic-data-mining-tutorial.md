---
title: Especifica el tipo de datos y el tipo de contenido (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 578d47783f22e857bb2fb84949e9d22dd6ad0e85
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174961"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>Especificar el tipo de datos y el tipo de contenido (Tutorial básico de minería de datos)
  Ahora que ha seleccionado qué columnas utilizar para generar la estructura y entrenar los modelos, realice los cambios necesarios en los datos predeterminados y tipos de contenido que establece el asistente.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>Revisar y modificar el tipo de contenido y el tipo de datos de cada columna  
  
1.  En el **contenido y el tipo de datos de columnas especificar** página, haga clic en **detectar** para ejecutar un algoritmo que determine los datos predeterminados y tipos de contenido para cada columna.  
  
2.  Revise las entradas de la **tipo de contenido** y **tipo de datos** columnas y cámbielas si es necesario, para asegurarse de que la configuración es los mismos que los que figuran en la tabla siguiente.  
  
     Normalmente, el asistente detectará números y asignará un tipo de datos numérico adecuado, pero hay varias situaciones en las que podría desear tratar un número como texto. Por ejemplo, el **GeographyKey** deben tratarse como texto, ya que no sería apropiado realizar operaciones matemáticas con este identificador.  
  
    |columna|Tipo de contenido|Tipo de datos|  
    |------------|------------------|---------------|  
    |**Línea de dirección 1**|**Discretos**|**Texto**|  
    |**Línea 2 de dirección**|**Discretos**|**Texto**|  
    |**Edad**|**Continua**|**Long**|  
    |**Bike Buyer**|**Discretos**|**Long**|  
    |**Commute Distance**|**Discretos**|**Texto**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**Continua**|**Date**|  
    |**Email Address**|**Discretos**|**Texto**|  
    |**English Education**|**Discretos**|**Texto**|  
    |**English Occupation**|**Discretos**|**Texto**|  
    |**firstName**|**Discretos**|**Texto**|  
    |**Sexo**|**Discretos**|**Texto**|  
    |**Clave geográfica**|**Discretos**|**Texto**|  
    |**House Owner Flag**|**Discretos**|**Texto**|  
    |**Last Name**|**Discretos**|**Texto**|  
    |**Marital Status**|**Discretos**|**Texto**|  
    |**Number Cars Owned**|**Discretos**|**Long**|  
    |**Number Children At Home**|**Discretos**|**Long**|  
    |**Region**|**Discretos**|**Texto**|  
    |**Total Children**|**Discretos**|**Long**|  
    |**Yearly Income**|**Continua**|**Doble**|  
  
3.  Haga clic en **Siguiente**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Especificar un conjunto de datos de prueba para la estructura &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Creación de una estructura de modelo de minería de datos de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de datos &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
