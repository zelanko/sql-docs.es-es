---
title: Colecciones integradas en expresiones (Generador de informes) | Microsoft Docs
description: Descubra las colecciones integradas en expresiones para hacer referencia a colecciones como parámetros, campos y conjuntos de datos de los informes en el Generador de informes.
ms.date: 3/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5dbc7cf2683f78118087d18b2dd51865bf52f3d
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84880259"
---
# <a name="built-in-collections-in-expressions-report-builder"></a>Colecciones integradas en expresiones (Generador de informes)
  En una expresión de un informe, puede incluir referencias a las siguientes colecciones integradas: ReportItems, Parameters, Fields, DataSets, DataSources, Variables y a campos integrados para información global, como el nombre del informe. No todas las colecciones aparecen en el cuadro de diálogo **Expresión** . Las colecciones DataSets y DataSources solo están disponibles en tiempo de ejecución para los informes publicados en un servidor de informes. ReportItems es una colección de cuadros de texto situados en una región del informe; por ejemplo, los cuadros de texto de una página o de un encabezado de página.  
  
 Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-built-in-collections"></a><a name="Collections"></a> Descripción de las colecciones integradas  
 En la tabla siguiente se enumeran las colecciones integradas disponibles cuando se escribe una expresión. Cada fila incluye: el nombre de programación para la colección con distinción de mayúsculas y minúsculas, si se puede usar el cuadro de diálogo Expresión para agregar una referencia a la colección de forma interactiva, un ejemplo y una descripción que incluye el momento en que se inicializan y se ponen a disposición de los usuarios los valores de la colección.  
  
|Colección integrada|Categoría en el cuadro de diálogo Expresión|Ejemplo|Descripción|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**Globales**|Campos integrados|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|Representa variables globales útiles para los informes, como el nombre del informe o el número de página. Siempre está disponible.<br /><br /> Para obtener más información, vea [Referencias a campos globales y de usuario integrados &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**User**|Campos integrados|`=User.UserID`<br /><br /> O bien<br /><br /> `=User.Language`|Representa una recopilación de datos acerca del usuario que ejecuta el informe, como la configuración de idioma o el identificador de usuario. Siempre está disponible.<br /><br /> Para obtener más información, vea [Referencias a campos globales y de usuario integrados &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).|  
|**Parámetros**|Parámetros|`=Parameters("ReportMonth").Value`<br /><br /> O bien<br /><br /> `=Parameters!ReportYear.Value`|Representa la colección de parámetros de informe (pueden tener uno o varios valores). No está disponible hasta que la inicialización se ha completado. Para más información, vea [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md).|  
|**Fields(** *\<Dataset>* **)**|Fields|`=Fields!Sales.Value`|Representa la colección de campos del conjunto de datos que están disponibles para el informe. Está disponible una vez que los datos se han recuperado desde un origen de datos en un conjunto de datos. Para obtener más información, vea [Referencias a la colección de campos de conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).|  
|**DataSets**|No se muestra|`=DataSets("TopEmployees").CommandText`|Representa la colección de conjuntos de datos a los que se hace referencia desde el cuerpo de una definición de informe. No incluye los orígenes de datos que solo se utilizan en encabezados o pies de página. No está disponible en el modo de vista previa local. Para más información, vea [Usar referencias a las colecciones DataSources y DataSets &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**DataSources**|No se muestra|`=DataSources("AdventureWorks2012").Type`|Representa la colección de orígenes de datos a los que se hace referencia en el cuerpo de un informe. No incluye los orígenes de datos que solo se utilizan en encabezados o pies de página. No está disponible en el modo de vista previa local. Para más información, vea [Usar referencias a las colecciones DataSources y DataSets &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md).|  
|**Variables**|`Variables`|`=Variables!CustomTimeStamp.Value`|Representa la colección de variables de informe y de variables de grupo. Para más información, vea [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md).|  
|**ReportItems**|No se muestra|`=ReportItems("Textbox1").Value`|Representa la colección de cuadros de texto para un elemento de informe. Esta colección se puede usar para resumir los elementos de la página a fin de incluirlos en un encabezado de página o en un pie de página. Para más información, vea [Usar referencias a la colección ReportItems &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md).|  
  
##  <a name="using-collection-syntax-in-an-expression"></a><a name="Syntax"></a> Uso de la sintaxis de colección en una expresión  
 Si desea hacer referencia a una colección desde una expresión, puede usar la sintaxis estándar de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para los elementos de una colección. En la tabla siguiente se muestran ejemplos de sintaxis de colección.  
  
|Sintaxis|Ejemplo|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>Consulte también  
 [Agregar una expresión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
