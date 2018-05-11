---
title: Establece el tipo de datos de una columna | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 65bfdd640305ec19fe50af09070e47a39b22ee3a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="set-the-data-type-of-a-column"></a>Establecer el tipo de datos de una columna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
-   **Texto**  
  
-   **Decimal Number**  
  
-   **Whole Number**  
  
-   **Moneda**  
  
-   **TRUE/FALSE**  
  
-   **Date**  
  
 Si encuentra que sus datos tienen un tipo de datos equivocado, o al menos diferente al que deseaba, tiene varias opciones:  
  
-   Puede reimportar los datos. Para ello, abra la conexión existente con el origen de datos y vuelva a importar la columna. En función del tipo de origen de datos, puede aplicar un filtro durante la importación para quitar los valores problemáticos.  
  
-   Puede crear una fórmula de DAX en una columna calculada para crear un nuevo valor del tipo de datos deseado. Por ejemplo, la función TRUNC se puede utilizar para convertir un número decimal en un número entero, o puede combinar funciones de información y funciones lógicas para probar y convertir los valores.  
  
### <a name="understanding-data-conversion"></a>Conversión de datos  
 Si se produce un error al seleccionar una opción de conversión de datos, podría ser que el tipo de datos actual de la columna no admitiera la conversión seleccionada. No todas las conversiones se permiten con todos los tipos de datos. Por ejemplo, solo puede cambiar una columna a un tipo de datos Boolean si el tipo de datos actual de la misma es un número (entero o decimal) o texto. Por consiguiente, debe elegir un tipo de datos adecuado para los datos de la columna.  
  
 Después de elegir un tipo de datos adecuado, el diseñador de modelos generará una advertencia sobre los posibles cambios en los datos, como por ejemplo, pérdida de precisión o truncamiento. Haga clic en Aceptar para aceptar y cambiar los datos al nuevo tipo de datos.  
  
 Si se admite el tipo de datos, pero el diseñador de modelos detecta valores que no se admiten en el nuevo tipo de datos, obtendrá otro error y deberá corregir los valores de datos antes de continuar.  
  
 Para obtener información detallada sobre los tipos de datos que se utilizan en modelos semánticos de business intelligence, cómo son tipos de datos convierten implícitamente y cómo diferentes se utiliza en las fórmulas, consulte [tipos de datos compatibles](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos compatibles](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)  
  
  
