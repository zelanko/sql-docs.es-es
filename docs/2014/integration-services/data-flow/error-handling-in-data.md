---
title: Control de errores en los datos| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827155"
---
# <a name="error-handling-in-data"></a>Control de errores en los datos
  Cuando un componente de flujo de datos aplica una transformación a los datos de columna, extrae datos de orígenes o carga datos en destinos, pueden producirse errores. Los errores con frecuencia se producen debido a valores de datos inesperados. Por ejemplo, una conversión de datos genera un error porque una columna contiene una cadena en lugar de un número, una inserción en una base de datos genera un error porque los datos corresponden a una fecha y la columna tiene un tipo de datos numéricos, o una expresión genera un error al evaluarse porque el valor de la columna es cero, lo que da como resultado una operación matemática no válida.  
  
 Los errores normalmente corresponden a una de las siguientes categorías:  
  
-   Errores de conversión de datos, que se producen cuando la conversión tiene como resultado la pérdida de dígitos significativos, la pérdida de dígitos insignificantes y el truncamiento de cadenas. Los errores de conversión de datos también se producen si la conversión requerida no se admite.  
  
-   Errores de evaluación de expresiones, que se producen si las expresiones que se evalúan en tiempo de ejecución realizan operaciones no válidas o pasan a ser sintácticamente incorrectas debido a valores de datos faltantes o incorrectos.  
  
-   Errores de búsqueda, que se producen si una operación de búsqueda genera un error al intentar buscar una coincidencia en la tabla de búsqueda.  
  
 Muchos componentes de flujo de datos admiten salidas de error, que le permiten controlar la forma en que el componente controla los errores de nivel de fila en los datos entrantes y salientes. El modo en que se comporta el componente cuando se produce un truncamiento o error se especifica estableciendo opciones en columnas individuales en la entrada o la salida. Por ejemplo, puede especificar que el componente genere un error si se truncan los datos de nombre del cliente, pero que omita los errores en otra columna que contenga datos menos importantes.  
  
 La salida de error se puede conectar a la entrada de otra transformación o cargarse en un destino diferente de la salida que no es de error. Por ejemplo, la salida de error puede estar conectada a una transformación Columna derivada que proporciona una cadena para una columna en blanco.  
  
 El siguiente diagrama muestra un flujo de datos simple que incluye una salida de error.  
  
 ![Flujo de datos con salida de error](../media/mw-dts-11.gif "Flujo de datos con salida de error")  
  
 Además de las columnas de datos, la salida de error incluye las columnas **ErrorCode** y **ErrorColumn** . La columna **ErrorCode** identifica el error y la columna **ErrorColumn** contiene el identificador de linaje de la columna de error. Para ver los metadatos de estas columnas, haga clic en la ruta que conecta la salida de error al siguiente componente en el flujo de datos. En algunas circunstancias, el valor de la columna **ErrorColumn** se establece en cero. Esto ocurre cuando la condición de error afecta a toda la fila en lugar de a una única columna. Un ejemplo es cuando se produce un error de búsqueda en la transformación Búsqueda.  
  
 Para obtener más información, vea [Flujo de datos](data-flow.md) y [Rutas de Integration Services](integration-services-paths.md).  
  
 Para obtener una lista de los errores, advertencias y otros mensajes de Integration Services, vea [Integration Services Error and Message Reference](../integration-services-error-and-message-reference.md).  
  
## <a name="error-and-truncation-options"></a>Opciones de errores y truncamiento  
 Los errores se asocian a una de estas dos categorías: errores o truncamientos. Un error indica un error inequívoco y genera un resultado NULL. Tales errores pueden incluir errores de conversión de datos o errores de evaluación de expresiones. Por ejemplo, un intento para convertir una cadena que contiene caracteres alfabéticos en un número produce un error. Las conversiones de datos, evaluaciones de expresiones y asignaciones de resultados de expresiones a variables, propiedades y columnas de datos pueden dar error debido a conversiones no válidas y tipos de datos incompatibles. Para obtener más información, vea [Conversión &#40;expresión de SSIS&#41;](../expressions/cast-ssis-expression.md), [Tipos de datos de Integration Services en las expresiones](../expressions/integration-services-data-types-in-expressions.md) y [Tipos de datos de Integration Services](integration-services-data-types.md).  
  
 Un truncamiento es de menor gravedad que un error. Un truncamiento genera resultados se pueden utilizar o que inclusive pueden ser beneficiosos. Puede elegir tratar los truncamientos como errores o como condiciones aceptables. Por ejemplo, si está insertando una cadena de 15 caracteres en una columna que solo tiene un carácter de ancho, puede elegir truncar la cadena.  
  
 Puede configurar la manera en que los orígenes, transformaciones y destinos controlan errores y truncamientos. Las opciones se describen en la siguiente tabla.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Error de componente|La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. El error es la opción predeterminada para un error o truncamiento.|  
|Omitir error|El error o truncamiento se omite y la fila de datos se dirige a la salida de transformación u origen.|  
|Redirigir fila|La fila de datos de error o truncamiento se dirige a la salida de error del origen, transformación o destino.|  
  
## <a name="adding-the-error-description"></a>Agregar la descripción del error  
 De forma predeterminada, una salida de error proporciona el código de error numérico y generalmente contiene el identificador de la columna en la que ocurrió el error. Puede utilizar el componente de script para incluir la descripción del error en una columna adicional mediante el uso de una única línea del script para llamar al método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> de la interfaz <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>.  
  
 El componente de script se puede agregar al segmento de error del flujo de datos en cualquier componente de nivel inferior de los componentes de flujo de datos cuyos errores desea capturar, pero generalmente se ubica inmediatamente antes de las filas de error escritas para un destino. De esta manera, el script solo busca descripciones para filas de error escritas. Por ejemplo, el segmento de error del flujo de datos puede corregir algunos errores y no escribir esas filas para un destino de error. Para obtener más información, vea [mejorar una salida de error con el componente de script](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md).  
  
### <a name="to-configure-an-error-output"></a>Para configurar una salida de error  
  
-   [Configurar una salida de error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](data-flow.md)   
 [Transformar datos con transformaciones](transformations/transform-data-with-transformations.md)   
 [Conectar componentes con rutas de acceso](../connect-components-with-paths.md)   
 [Tarea flujo de datos](../control-flow/data-flow-task.md)   
 [Flujo de datos](data-flow.md)  
  
  
