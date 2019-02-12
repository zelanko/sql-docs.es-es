---
title: Especifica el tipo de datos y el tipo de contenido (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040212"
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
    |**Edad**|**continua**|**Long**|  
    |**Bike Buyer**|**Discretos**|**Long**|  
    |**Commute Distance**|**Discretos**|**Texto**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**continua**|**Date**|  
    |**Email Address**|**Discretos**|**Texto**|  
    |**English Education**|**Discretos**|**Texto**|  
    |**English Occupation**|**Discretos**|**Texto**|  
    |**FirstName**|**Discretos**|**Texto**|  
    |**Sexo**|**Discretos**|**Texto**|  
    |**Clave geográfica**|**Discretos**|**Texto**|  
    |**House Owner Flag**|**Discretos**|**Texto**|  
    |**Last Name**|**Discretos**|**Texto**|  
    |**Marital Status**|**Discretos**|**Texto**|  
    |**Number Cars Owned**|**Discretos**|**Long**|  
    |**Number Children At Home**|**Discretos**|**Long**|  
    |**Region**|**Discretos**|**Texto**|  
    |**Total Children**|**Discretos**|**Long**|  
    |**Yearly Income**|**continua**|**Doble**|  
  
3.  Haga clic en **Siguiente**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Especificar un conjunto de datos de prueba para la estructura &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Creación de una estructura de modelo de minería de datos de distribución de correo directo &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de datos &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
