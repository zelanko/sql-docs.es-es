---
title: "rsProcessingError - Error de Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rsProcessingError"
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
caps.latest.revision: 29
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 29
---
# rsProcessingError - Error de Reporting Services
    
## Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|rsProcessingError|  
|Origen del evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|Error al procesar el informe.|  
  
## Explicación  
 Se encontraron uno o varios errores al publicar, procesar, obtener una vista previa localmente, ver desde el servidor de informes, o crear una suscripción para un informe. Este mensaje de error indica que se ha detectado, como mínimo, un error.  
  
### Posibles causas  
 Las causas posibles incluyen:  
  
-   Se ha producido un error de procesamiento en el servidor de informes.  
  
-   Se ha producido un error de procesamiento durante el procesamiento local de informes al obtener una vista previa del informe.  
  
-   El resultado de la evaluación de una expresión de grupo es un tipo de datos incorrecto.  
  
-   Una definición de filtro especificaba dos expresiones que se evaluaron como tipos de datos que no se pudieron comparar.  
  
-   Una expresión hace referencia a un campo no existente en la colección de campos.  
  
-   Una expresión incluía una llamada a una función de agregado con un ámbito no válido o en conflicto.  
  
-   Una expresión hacía referencia a un parámetro no existente en la colección Parámetros del informe.  
  
-   No se pudo cargar un ensamblado personalizado o un ensamblado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que estaba implementado incorrectamente.  
  
-   Se ha detectado que un parámetro con el conjunto de propiedades que admite valores NULL establecido en **False** tiene un valor NULL en el parámetro.  
  
-   Una expresión para la propiedad Hidden de una región de datos contiene un error: Referencia de objeto no definida a una instancia de un objeto.  
  
-   Una expresión incluía una llamada de función no válida o un error de sintaxis.  
  
## Acción del usuario  
  
### Buscar más información  
 Realice una o más de las acciones siguientes:  
  
-   Si ve el informe desde el servidor de informes o como una suscripción, lea todo el texto del mensaje de error. En él se proporciona información adicional.  
  
-   Si está creando un informe en el Diseñador de informes y observa este error al obtener una vista previa o al publicar el informe, se proporcionará información adicional en la ventana Lista de errores.  
  
-   Si está creando un informe en Report Designer Preview, lea todo el texto del mensaje de error. En él se proporciona información adicional.  
  
-   Si está viendo un informe como administrador local en el servidor de informes, puede ver la pila de llamadas si hace clic con el botón derecho en la página y selecciona **Ver código fuente**. En ella se proporciona información adicional.  
  
-   Si actúa como administrador local en el servidor de informes, busque `ReportProcessingException`en el archivo de registro. Las entradas del registro contienen más información. El archivo de registro del servidor de informes suele encontrarse en \<*unidad*>:\Archivos de programa\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*marcaDeFechaYHora*.log. Para más información, vea [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
### Error al cargar el ensamblado de expresiones  
 Los ensamblados personalizados necesitan tener un nombre seguro y el atributo AllowPartiallyTrustedCallers establecido. Para obtener más información, consulte [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) y [Understanding Security Policies](../../reporting-services/extensions/secure-development/understanding-security-policies.md).  
  
### Un nombre global integrado no existe  
 Compruebe la ortografía de las expresiones. En los parámetros y nombres de campo globales integrados se distinguen mayúsculas de minúsculas. En la expresión que produce el error, compruebe que el nombre existe realmente en el informe y que está escrito con la grafía correcta. Para más información, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder-and-ssrs.md).  
  
### Propiedades de parámetros y NULL  
 Los parámetros de varios valores no pueden ser NULL. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
### No se puede procesar el informe principal con subinforme  
 La misma versión del procesador de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] debe procesar un informe con subinformes. Al actualizar los informes a la versión actual del esquema de definición de informe, el informe principal y los subinformes pueden actualizarse o no al mismo tiempo. Si la versión no es compatible entre un informe y sus subinformes, se muestra el mensaje siguiente: "No se pudo procesar el subinforme".  
  
 Debe cambiar el informe principal o los subinformes para que todos los informes se puedan procesar con la misma versión del procesador de informes. Para obtener información sobre los motivos por los que no se puede actualizar un informe, vea [Actualizar informes](../../reporting-services/install-windows/upgrade-reports.md).  
  
### Compruebe que las llamadas a funciones son de Visual Basic y no de SQL  
 Puede utilizar funciones SQL en el texto de consulta en una base de datos relacional. No puede utilizar las funciones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] en texto de consulta.  
  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], las expresiones pueden utilizar las funciones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , las funciones de System.Math o System.String, las funciones completas de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , o las funciones personalizadas que se proporcionen en un código o ensamblado personalizado. No puede utilizar funciones SQL en una expresión.  
  
 Compruebe que las llamadas a funciones realizadas en la consulta y en las expresiones son válidas.  
  
### No se pueden comparar los tipos de datos para un filtro  
 En una ecuación de filtro, la expresión de filtro que define lo que se ha de filtrar y el valor de filtro deben ser del mismo tipo de datos para poder compararse. Si ve alguno de los errores siguientes, modifique la expresión de campo o el valor de filtro para que los tipos de datos coincidan:  
  
-   No se puede realizar el procesamiento de *\<tipo de elemento de informe>* para el *\<nombre de elemento de informe>*. No se pueden comparar los datos de los tipos *\<tipo>* y *\<tipo>*. Compruebe el tipo de datos devuelto por el *\<nombre de elemento de informe>*.  
  
-   Error al evaluar el *\<nombre de propiedad>*.  
  
-   Error al evaluar el *\<nombre de propiedad>*. Hace referencia a un campo de conjunto de datos que contiene un error: *\<cadena de error>*.  
  
 Para más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### Especificación no válida o de ámbito en conflicto en la llamada a una función de agregado  
 Al incluir llamadas a funciones de agregado en una expresión de una celda Tablix, el procesador de informes evalúa la expresión en el ámbito de los grupos más internos a los que pertenece la celda.  
  
 También se puede pasar el nombre de un ámbito concreto a una función de agregado. El ámbito puede hacer referencia al nombre de un conjunto de datos, una región de datos o el nombre un ámbito superior en la jerarquía de datos. Esto se aplica a los mensajes siguientes:  
  
-   El *\<tipo de elemento de informe>* “*\<nombre de elemento de informe>*” tiene un ámbito no válido nombre de ámbito “*\<nombre de ámbito>*”. El ámbito debe ser el actual o estar dentro del actual.  
  
-   La expresión *\<nombre de propiedad>* para el *\<tipo de elemento de informe>* “*\<nombre de elemento de informe>*” tiene un parámetro de ámbito que no es válido para una función de agregado. El parámetro de ámbito debe establecerse en una constante de cadena que sea igual al nombre de un grupo contenedor, al nombre de una región de datos contenedora o al nombre de un conjunto de datos.  
  
 Para las funciones de agregado que calculan totales acumulados (**Previous**, **RunningValue** o **RowNumber**), se puede especificar un parámetro de ámbito que sea un nombre de grupo de filas o de grupo de columnas, pero no ambos. Esto se aplica al mensaje de error siguiente:  
  
-   Las funciones de agregado **Previous**, **RunningValue** o **RowNumber** usadas en las celdas de datos del *\<tipo de elemento de informe>* “*\<nombre de elemento de informe>*” hacen referencia a ámbitos de agrupación en las columnas y filas de *\<tipo de elemento de informe>*. Los parámetros de ámbito de todas las funciones de agregado **Previous**, **RunningValue** y **RowNumber** de *\<tipo de elemento de informe>* pueden hacer referencia a agrupaciones de filas o agrupaciones de columnas de datos, pero no a ambos.  
  
 Para más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md) y [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder-and-ssrs.md).  
  
### Ámbito del conjunto de datos predeterminado para un cuadro de texto de nivel superior  
 No utilice un ámbito predeterminado para un cuadro de texto agregado a la superficie de diseño del informe cuando éste tenga más de un conjunto de datos. Utilice una expresión que incluya el nombre del conjunto de datos como ámbito, y una función de agregado. Por ejemplo, `=First(Fields!FieldName.Value, "DataSet2")`.  
  
## Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Filtros de uso frecuente &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/parameters-collection-references-report-builder-and-ssrs.md)  
  
  