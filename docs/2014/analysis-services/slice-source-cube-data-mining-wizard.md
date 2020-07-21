---
title: Segmentar el cubo de origen (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
ms.openlocfilehash: 762248d4c2a268ac36b0dfa3ffeba20123017017
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940506"
---
# <a name="slice-source-cube-data-mining-wizard"></a>Segmentar el cubo de origen (Asistente para minería de datos)
  Puede utilizar el cuadro de diálogo **Segmentar el cubo de origen** para restringir los datos usados para entrenar el modelo. Un cubo suele contener datos relacionados con muchas dimensiones y atributos diferentes, como todas las tiendas, todas las regiones y todos los productos. No resulta práctico entrenar un modelo en combinaciones ilimitadas de atributos, por lo que debe utilizar este cuadro de diálogo para elegir un conjunto específico que se empleará para entrenar un modelo.  
  
 Por ejemplo, en el cubo de AdventureWorks, puede segmentar por una línea de producto, una región o un año determinados para obtener una parte de los datos.  
  
 Si no está familiarizado con los segmentos y los cubos, se recomienda que revise los siguientes artículos:  
  
-   [Establezca la propiedad segmento de partición &#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [Crear y administrar una partición local &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  Tenga en cuenta que las funciones MDX dinámicas (como [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) o [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function)) no son compatibles con la propiedad Slice para particiones. Debe definir el segmento utilizando tuplas explícitas o referencias de miembro.  
>   
>  Por ejemplo, en lugar de usar [: &#40;intervalo&#41; &#40;MDX&#41;](/sql/mdx/range-mdx) para definir un intervalo, necesitaría enumerar cada miembro por los años específicos.  
>   
>  Si necesita definir un segmento complejo, se recomienda definir las tuplas del segmento con un script Alter de XMLA. Después, puede usar la herramienta de línea de comandos ascmd o la tarea SSIS [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) para ejecutar el script y crear el conjunto de miembros especificado inmediatamente antes de procesar la partición.  
  
 **Para más información:** [Asistente para minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Crear una estructura de minería de datos relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opciones  
 **Dimensión**  
 Seleccione la dimensión que desea segmentar.  
  
 **Hierarchy**  
 Seleccione la jerarquía que desea segmentar. Puede elegir cualquier nivel de una jerarquía, pero los atributos utilizados en el modelo solo estarán en el nivel que elija.  
  
 Por ejemplo, si elige la jerarquía Geography y selecciona Country como nivel, no puede crear un modelo que use City como atributo. Por el contrario, si elige City como el nivel de la jerarquía para segmentar, no puede crear un modelo de minería de datos basado en Country.  
  
 **Operador**  
 Seleccione el operador que desea utilizar para generar una expresión de segmentación.  
  
 Por ejemplo, si elige Geography como jerarquía, puede seleccionar el operador = y, a continuación, escribir "Europe" como filtro para obtener datos del cubo solo para Europa.  
  
 **Expresión de filtro**  
 Escriba una expresión que se usará como criterio para filtrar el cubo en la dimensión seleccionada.  
  
 **Parámetros**  
 Esta opción no se utiliza para los modelos de minería de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Finalización del asistente &#40;Asistente para minería de datos&#41;](completing-the-wizard-data-mining-wizard.md)   
 [Asistente para minería de datos (ayuda F1) &#40;Analysis Services: minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Especificar el uso de la columna del modelo de minería de datos &#40;Asistente para minería de datos&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
