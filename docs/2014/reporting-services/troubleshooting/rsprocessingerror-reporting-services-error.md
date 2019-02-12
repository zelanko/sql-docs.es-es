---
title: rsProcessingError - Error de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f7c364708f3d574f5096210a94fc33174b3eb2c2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021560"
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Error de Reporting Services
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|rsProcessingError|  
|Origen del evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|Error al procesar el informe.|  
  
## <a name="explanation"></a>Explicación  
 Se encontraron uno o varios errores al publicar, procesar, obtener una vista previa localmente, ver desde el servidor de informes, o crear una suscripción para un informe. Este mensaje de error indica que se ha detectado, como mínimo, un error.  
  
### <a name="possible-causes"></a>Posibles causas  
 Las causas posibles incluyen:  
  
-   Se ha producido un error de procesamiento en el servidor de informes.  
  
-   Se ha producido un error de procesamiento durante el procesamiento local de informes al obtener una vista previa del informe.  
  
-   El resultado de la evaluación de una expresión de grupo es un tipo de datos incorrecto.  
  
-   Una definición de filtro especificaba dos expresiones que se evaluaron como tipos de datos que no se pudieron comparar.  
  
-   Una expresión hace referencia a un campo no existente en la colección de campos.  
  
-   Una expresión incluía una llamada a una función de agregado con un ámbito no válido o en conflicto.  
  
-   Una expresión hacía referencia a un parámetro no existente en la colección Parámetros del informe.  
  
-   No se pudo cargar un ensamblado personalizado o un ensamblado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estaba implementado incorrectamente.  
  
-   Un parámetro que tiene la propiedad que acepta valores NULL en `False` ha detectado un valor null en el parámetro.  
  
-   Una expresión para la propiedad Hidden de una región de datos contiene un error: Referencia de objeto no definida a una instancia de un objeto.  
  
-   Una expresión incluía una llamada de función no válida o un error de sintaxis.  
  
## <a name="user-action"></a>Acción del usuario  
  
### <a name="finding-more-information"></a>Buscar más información  
 Realice una o más de las acciones siguientes:  
  
-   Si ve el informe desde el servidor de informes o como una suscripción, lea todo el texto del mensaje de error. En él se proporciona información adicional.  
  
-   Si está creando un informe en el Diseñador de informes y observa este error al obtener una vista previa o al publicar el informe, se proporcionará información adicional en la ventana Lista de errores.  
  
-   Si está creando un informe en Report Designer Preview, lea todo el texto del mensaje de error. En él se proporciona información adicional.  
  
-   Si está viendo un informe como administrador local en el servidor de informes, puede ver la pila de llamadas si hace clic con el botón derecho en la página y selecciona **Ver código fuente**. En ella se proporciona información adicional.  
  
-   Si actúa como administrador local en el servidor de informes, busque `ReportProcessingException`en el archivo de registro. Las entradas del registro contienen más información. El archivo de registro del servidor de informes suele encontrarse en \<*unidad*>:\Archivos de programa\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*marcaDeFechaYHora*.log. Para más información, vea [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
### <a name="failed-to-load-expression-host-assembly"></a>Error al cargar el ensamblado de expresiones  
 Los ensamblados personalizados necesitan tener un nombre seguro y el atributo AllowPartiallyTrustedCallers establecido. Para obtener más información, consulte [Using Custom Assemblies with Reports](../custom-assemblies/using-custom-assemblies-with-reports.md) y [Understanding Security Policies](../extensions/secure-development/understanding-security-policies.md).  
  
### <a name="a-built-in-global-name-does-not-exist"></a>Un nombre global integrado no existe  
 Compruebe la ortografía de las expresiones. En los parámetros y nombres de campo globales integrados se distinguen mayúsculas de minúsculas. En la expresión que produce el error, compruebe que el nombre existe realmente en el informe y que está escrito con la grafía correcta. Para obtener más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="parameter-properties-and-null"></a>Propiedades de parámetros y NULL  
 Los parámetros de varios valores no pueden ser NULL. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>No se puede procesar el informe principal con subinforme  
 La misma versión del procesador de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debe procesar un informe con subinformes. Al actualizar los informes a la versión actual del esquema de definición de informe, el informe principal y los subinformes pueden actualizarse o no al mismo tiempo. Si la versión no es compatible entre un informe y sus subinformes, se muestra el mensaje siguiente: "No se pudo procesar el subinforme".  
  
 Debe cambiar el informe principal o los subinformes para que todos los informes se puedan procesar con la misma versión del procesador de informes. Para obtener información sobre los motivos por los que no se puede actualizar un informe, vea [Actualizar informes](../install-windows/upgrade-reports.md).  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>Compruebe que las llamadas a funciones son de Visual Basic y no de SQL  
 Puede utilizar funciones SQL en el texto de consulta en una base de datos relacional. No puede utilizar las funciones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] en texto de consulta.  
  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], las expresiones pueden utilizar las funciones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , las funciones de System.Math o System.String, las funciones completas de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , o las funciones personalizadas que se proporcionen en un código o ensamblado personalizado. No puede utilizar funciones SQL en una expresión.  
  
 Compruebe que las llamadas a funciones realizadas en la consulta y en las expresiones son válidas.  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>No se pueden comparar los tipos de datos para un filtro  
 En una ecuación de filtro, la expresión de filtro que define lo que se ha de filtrar y el valor de filtro deben ser del mismo tipo de datos para poder compararse. Si ve alguno de los errores siguientes, modifique la expresión de campo o el valor de filtro para que los tipos de datos coincidan:  
  
-   No se puede efectuar el procesamiento de *\<tipo de elemento de informe>* del *\<nombre del elemento de informe>*. No se pueden comparar los datos de los tipos *\<tipo>* y *\<tipo>*. Compruebe el tipo de datos devuelto por el *\<nombre del elemento de informe>*.  
  
-   Error al evaluar el *\<nombre de propiedad>*.  
  
-   Error al evaluar el *\<nombre de propiedad>*. Hace referencia a un campo de conjunto de datos que contiene un error: *\<cadena de error>*.  
  
 Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>Especificación no válida o de ámbito en conflicto en la llamada a una función de agregado  
 Al incluir llamadas a funciones de agregado en una expresión de una celda Tablix, el procesador de informes evalúa la expresión en el ámbito de los grupos más internos a los que pertenece la celda.  
  
 También se puede pasar el nombre de un ámbito concreto a una función de agregado. El ámbito puede hacer referencia al nombre de un conjunto de datos, una región de datos o el nombre un ámbito superior en la jerarquía de datos. Esto se aplica a los mensajes siguientes:  
  
-   El *\<tipo de elemento de informe>* "*\<nombre de elemento de informe>*" tiene el ámbito no válido "*\<nombre de ámbito>*". El ámbito debe ser el actual o estar dentro del actual.  
  
-   La expresión *\<nombre de propiedad>* del *\<tipo de elemento de informe>* "*\<nombre de elemento de informe>*" tiene un parámetro de ámbito que no es válido para una función de agregado. El parámetro de ámbito debe establecerse en una constante de cadena que sea igual al nombre de un grupo contenedor, al nombre de una región de datos contenedora o al nombre de un conjunto de datos.  
  
 Para las funciones de agregado que calculan totales acumulados (`Previous`, `RunningValue` o `RowNumber`), se puede especificar un parámetro de ámbito que sea un nombre de grupo de filas o de grupo de columnas, pero no ambos. Esto se aplica al mensaje de error siguiente:  
  
-   `Previous`, `RunningValue` o `RowNumber` utilizadas en las celdas de datos de las funciones de agregado el  *\<tipo de elemento de informe >* '*\<el nombre del elemento de informe >*' hacen referencia a los ámbitos de agrupación en las columnas y filas de la  *\<tipo de elemento de informe >*. Los parámetros de ámbito de todos los `Previous`, `RunningValue` y `RowNumber` agregar funciones dentro de un  *\<tipo de elemento de informe >* puede hacer referencia a las agrupaciones de filas o agrupaciones de columnas de datos, pero no ambos.  
  
 Para más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) y [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>Ámbito del conjunto de datos predeterminado para un cuadro de texto de nivel superior  
 No utilice un ámbito predeterminado para un cuadro de texto agregado a la superficie de diseño del informe cuando éste tenga más de un conjunto de datos. Utilice una expresión que incluya el nombre del conjunto de datos como ámbito, y una función de agregado. Por ejemplo, `=First(Fields!FieldName.Value, "DataSet2")`.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](../report-data/report-datasets-ssrs.md)   
 [Filtros de uso frecuente &#40;Generador de informes y SSRS&#41;](../report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
