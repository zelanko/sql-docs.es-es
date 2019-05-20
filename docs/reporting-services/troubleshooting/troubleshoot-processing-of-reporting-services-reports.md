---
title: Solución de problemas de procesamiento de informes de Reporting Services | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: bb309231-68be-4d68-a44c-c098999c67a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 85486e929683abaf99216a4d4b03c19a146f230c
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65573870"
---
# <a name="troubleshoot-processing-of-reporting-services-reports"></a>Solución de problemas de procesamiento de informes de Reporting Services
Una vez recuperados los datos del informe, el procesador de informes combina los datos y la información de diseño. Cada propiedad de elemento de informe que tiene una expresión se evalúa en el contexto de los datos y el diseño combinados. Utilice este tema como ayuda para solucionar estos problemas.   
  
## <a name="my-report-definition-is-not-valid"></a>La definición de informe no es válida.  
En tiempo de ejecución, el procesador de informes combina los datos y los elementos de diseño en la definición de informe, y evalúa las expresiones para las propiedades de elemento de informe.   
  
El procesador de informes comprueba que la definición de informe (archivo .rdl) cumple el esquema que se especifica al principio de la declaración de espacio de nombres del archivo .rdl. Para más información sobre los esquemas RDL, vea [Buscar la versión del esquema de definición de informe (SSRS)](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
Además, las expresiones de informe que se evalúan en tiempo de ejecución deben seguir un conjunto de reglas que permitan asegurarse de que los datos del informe y el diseño se pueden combinar correctamente. Cuando el procesador de informes detecta un problema, podría ver el mensaje siguiente: La definición de `<report name>` del informe no es válida.  
  
### <a name="report-item-expressions-can-only-refer-to-fields-within-the-current-dataset-scope-or-if-inside-an-aggregate-the-specified-dataset-scope"></a>Las expresiones de elemento de informe solamente pueden hacer referencia a los campos dentro del ámbito del conjunto de datos actual o, si están dentro de un agregado, el ámbito del conjunto de datos especificado.  
  
Utilice la lista siguiente para ayudar a determinar la causa del error:  
* Cuando un informe tiene más de un conjunto de datos, una expresión agregada en un cuadro de texto del cuerpo del informe debe especificar un parámetro de ámbito. Por ejemplo, `=First(Fields!FieldName.Value, "DataSet1")`.  
  
Para especificar un parámetro de ámbito, proporcione el nombre de un conjunto de datos, región de datos o grupo que esté en el ámbito del elemento de informe. Para más información, consulte [Descripción del ámbito de expresión para totales, agregados y colecciones integradas (Generador de informes 3.0 y SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) y [Referencia a expresión (Generador de informes 3.0 y SSRS)](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md).  
  
### <a name="names-of-objects-must-be-greater-than-0-and-less-than-or-equal-to-256-characters"></a>El número de caracteres del nombre de los objetos debe ser mayor que 0 y menor o igual que 256.  
La longitud de los identificadores de objetos en una definición de informe está restringida a 256 caracteres. Los identificadores deben tener distinción entre mayúsculas y minúsculas y cumplir CLS. El nombre debe comenzar por una letra y estar compuesto de letras, números y un carácter de subrayado (_); además, no debe contener espacios. Por ejemplo, los nombres de los cuadros de texto o de las regiones de datos deben obedecer estas instrucciones.   
  
Para cambiar el nombre de un objeto, en la barra de herramientas del panel Propiedades, seleccione el elemento en la lista desplegable, desplácese a **Nombre** y escriba un nombre de objeto válido.   
  
## <a name="a-text-box-displays-error-how-do-i-fix-it"></a>Un cuadro de texto muestra "#Error"; ¿cómo lo corrijo?  
El mensaje "#Error" se produce cuando el procesador de informes evalúa las expresiones de las propiedades de elementos de informe en tiempo de ejecución y detecta un error de conversión de tipos de datos, ámbito o de otro tipo.   
  
Un error de tipo de datos normalmente significa que el valor predeterminado o el tipo de datos especificado no se admiten. Un error de ámbito significa que el ámbito especificado no estaba disponible en el momento en que se evaluó la expresión.   
  
Para eliminar el mensaje de error, debe rescribir la expresión que lo produce. Para determinar más detalles sobre el problema, vea el mensaje de error detallado.   
  
En la vista previa, en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)], vea la ventana Resultados. En el servidor de informes, vea la pila de llamadas. 
  
  
## <a name="see-also"></a>Consulte también  
[Errores y eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

