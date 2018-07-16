---
title: Establezca el tipo de datos de una columna (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 34e2d508-7b64-4503-a4f0-c6c6ad5f8a44
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d0871dbef7b9b9a053a7c79688ec7073d2d8fdcc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312235"
---
# <a name="set-the-data-type-of-a-column-ssas-tabular"></a>Establecer el tipo de datos de una columna (SSAS tabular)
  Cuando se importan o se pegan datos en un modelo, el diseñador de modelos detecta automáticamente los tipos de datos y los aplica. Después de haber agregado los datos al modelo, puede modificar manualmente el tipo de datos de una columna para cambiar el modo en que se almacenan los datos. Si solo desea cambiar el formato de visualización de los datos sin cambiar la forma de almacenarlos, puede hacer eso en su lugar.  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>Para cambiar el tipo de datos o el formato de presentación de una columna  
  
1.  En el diseñador de modelos, seleccione la columna cuyo tipo de datos o formato de presentación desea cambiar.  
  
2.  En la ventana **Propiedades** , realice una de las acciones siguientes:  
  
    -   En la propiedad **Formato de datos** , seleccione un formato de datos diferente.  
  
    -   En la propiedad **Tipo de datos** , seleccione un tipo de datos diferente.  
  
## <a name="considerations-when-changing-data-types"></a>Consideraciones sobre la modificación de los tipos de datos  
 En ocasiones, al intentar cambiar el tipo de datos de una columna o seleccionar una conversión de datos, se podrían producir uno de los siguientes errores:  
  
-   Error al cambiar el tipo de datos  
  
-   Error al cambiar el tipo de datos de la columna  
  
 Estos errores se podrían producir aun cuando el tipo de datos está disponible como una opción en la lista desplegable Tipo de datos. En esta sección se explica la causa de estos errores y cómo pueden corregirse.  
  
### <a name="understanding-automatically-determined-data-types"></a>Descripción de los tipos de datos que se determinan automáticamente  
 Al agregar los datos a un modelo, el diseñador de modelos comprueba las columnas de datos para ver qué tipos de datos contiene cada columna. Si los datos en esa columna son coherentes, se asigna a la columna el tipo de datos más preciso.  
  
 Sin embargo, si agrega datos de Excel o de otro origen que no exija usar un tipo de datos único dentro de cada columna, el diseñador de modelos asignará un tipo de datos que dé cabida a todos los valores dentro de la columna. Por consiguiente, si una columna contiene números de tipos diferentes, como enteros, números de tipo long y moneda, el diseñador de modelos usará un tipo de datos decimal. De forma alternativa, si una columna mezcla números y texto, el diseñador de modelos usará el tipo de datos de texto. El diseñador de modelos no proporciona un tipo de datos similar al tipo de datos General disponible en Excel.  
  
 Por consiguiente, si una columna contiene valores numéricos y de texto, no podrá convertirla en un tipo de datos numérico.  
  
 Los tipos de datos siguientes están disponibles en los modelos semánticos de Business Intelligence:  
  
|Tipos de datos de los modelos|  
|----------------------|  
|Texto<br /><br /> Decimal Number<br /><br /> Whole Number<br /><br /> Moneda<br /><br /> TRUE/FALSE<br /><br /> date|  
  
 Si encuentra que sus datos tienen un tipo de datos equivocado, o al menos diferente al que deseaba, tiene varias opciones:  
  
-   Puede reimportar los datos. Para ello, abra la conexión existente con el origen de datos y vuelva a importar la columna. En función del tipo de origen de datos, puede aplicar un filtro durante la importación para quitar los valores problemáticos.  
  
-   Puede crear una fórmula de DAX en una columna calculada para crear un nuevo valor del tipo de datos deseado. Por ejemplo, la función TRUNC se puede utilizar para convertir un número decimal en un número entero, o puede combinar funciones de información y funciones lógicas para probar y convertir los valores.  
  
### <a name="understanding-data-conversion"></a>Conversión de datos  
 Si se produce un error al seleccionar una opción de conversión de datos, podría ser que el tipo de datos actual de la columna no admitiera la conversión seleccionada. No todas las conversiones se permiten con todos los tipos de datos. Por ejemplo, solo puede cambiar una columna a un tipo de datos Boolean si el tipo de datos actual de la misma es un número (entero o decimal) o texto. Por consiguiente, debe elegir un tipo de datos adecuado para los datos de la columna.  
  
 Después de elegir un tipo de datos adecuado, el diseñador de modelos generará una advertencia sobre los posibles cambios en los datos, como por ejemplo, pérdida de precisión o truncamiento. Haga clic en Aceptar para aceptar y cambiar los datos al nuevo tipo de datos.  
  
 Si se admite el tipo de datos, pero el diseñador de modelos detecta valores que no se admiten en el nuevo tipo de datos, obtendrá otro error y deberá corregir los valores de datos antes de continuar.  
  
 Para obtener información detallada sobre los tipos de datos que se usan en los modelos semánticos de Business Intelligence, cómo se convierten implícitamente y cómo se usan los diferentes tipos de datos en las fórmulas, vea [Data Types Supported &#40;SSAS Tabular&#41;](data-types-supported-ssas-tabular.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos admitidos &#40;Tabular de SSAS&#41;](data-types-supported-ssas-tabular.md)  
  
  
