---
title: "Establecer la propiedad de división de particiones (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0dc6d3620e26186c57a78ddb88e44548384c7b7d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-the-partition-slice-property-analysis-services"></a>Establecer la propiedad Slice de particiones (Analysis Services)
  Un segmento de datos es una característica de optimización importante que ayuda a dirigir consultas a los datos de las particiones adecuadas. Establecer explícitamente la propiedad Slice puede mejorar el rendimiento de las consultas invalidando los sectores predeterminados generados para las particiones MOLAP y ROLAP. Además, la propiedad Slice proporciona una comprobación de validación adicional al procesar la partición.  
  
 Puede especificar un segmento de datos después de crear una partición, pero antes de procesarla, mediante la propiedad Slice. En la pestaña Particiones, expanda un grupo de medida, haga clic con el botón derecho en una partición y seleccione **Propiedades**.  
  
 Para obtener una explicación de las ventajas de los segmentos de datos, vea [Establecer el segmento en una partición de un cubo de SSAS](http://go.microsoft.com/fwlink/?LinkId=317783).  
  
## <a name="defining-a-slice"></a>Definir un segmento  
 Los valores válidos para una propiedad Slice es un miembro, un conjunto o una tupla de MDX. En los ejemplos siguientes se ilustra la sintaxis válida de Slice:  
  
|Segmento|Miembro, conjunto o tupla|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|Especifique este segmento en una partición que contenga hechos desde el año 2010 (suponiendo que el modelo incluya una dimensión Date con una jerarquía Calendar Year, donde 2010 sea un miembro). Aunque la cláusula WHERE o la tabla de origen de la partición puede estar ya filtrada por 2010, al especificar el segmento se ofrece una comprobación adicional durante el procesamiento, así como recorridos más dirigidos durante la ejecución de las consultas.|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|Especifique este segmento en una partición que contenga hechos que incluyan información de territorios de ventas. Un segmento puede ser un conjunto MDX que consta de dos o más miembros.|  
|[Measures].[Sales Amount Quota] > '5000'|Este segmento muestra una expresión MDX.|  
  
 Un sector de datos de una partición debería reflejar lo más fielmente posible los datos de la partición. Por ejemplo, si una partición está limitada a los datos de 2012, el segmento de datos de la partición debería especificar el miembro 2012 de la dimensión de tiempo. No siempre es posible especificar un segmento de datos que refleje el contenido exacto de una partición. Por ejemplo, si una partición contiene datos solamente para enero y febrero, pero los niveles de la dimensión de tiempo son año, trimestre y mes, el Asistente para particiones no puede seleccionar los miembros de enero y febrero a la vez. En estos casos, seleccione el miembro primario de los miembros que reflejen el contenido de la partición. En este ejemplo, seleccione el trimestre 1.  
  
> [!NOTE]  
>  Tenga en cuenta que las funciones MDX dinámicas (como [Generate &#40;MDX&#41;](../../mdx/generate-mdx.md) o [Except &#40;MDX&#41;](../../mdx/except-mdx-function.md)) no son compatibles con la propiedad Slice para particiones. Debe definir el segmento utilizando tuplas explícitas o referencias de miembro.  
>   
>  Por ejemplo, en lugar de usar el operador de intervalo (:) para definir un intervalo, tendría que enumerar cada miembro por los años específicos.  
>   
>  Si necesita definir un segmento complejo, se recomienda definir las tuplas del segmento con un script Alter de XMLA. Después, puede usar la herramienta de línea de comandos ascmd o la [Tarea Ejecutar DDL de Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) de Integration Services para ejecutar el script y crear el conjunto especificado de miembros inmediatamente antes de procesar la partición.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  

