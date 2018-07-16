---
title: Comparar datos de cadena | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c5c471942764076ac0c03044d1037c3600e83fc5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280311"
---
# <a name="comparing-string-data"></a>comparar datos de cadena
  Las comparaciones de cadenas son una parte importante de muchas de las transformaciones realizadas por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], y las comparaciones de cadenas también se utilizan en la evaluación de expresiones en variables y expresiones de propiedades. Por ejemplo, la transformación Ordenar compara valores en un conjunto de datos para ordenar datos en orden ascendente o descendente.  
  
## <a name="configuring-transformations-for-string-comparisons"></a>Configurar transformaciones para las comparaciones de cadenas  
 Las transformaciones Ordenar, Agregado, Agrupación aproximada y Búsqueda aproximada se pueden personalizar para cambiar la manera en que se comparan las cadenas en el nivel de columna. Por ejemplo, se puede especificar que una comparación omita la distinción entre mayúsculas y minúsculas, lo que significa que los caracteres en mayúscula o minúscula se tratan como si fueran el mismo carácter.  
  
 Las siguientes transformaciones usan expresiones que pueden incluir comparaciones de cadenas.  
  
-   La transformación División condicional puede usar comparaciones de cadenas en expresiones para determinar a qué salida se debe enviar la fila de datos. Para más información, consulte [Conditional Split Transformation](transformations/conditional-split-transformation.md).  
  
-   La transformación Columna derivada puede usar comparaciones de cadenas en expresiones para generar nuevos valores de columna. Para más información, consulte [Derived Column Transformation](transformations/derived-column-transformation.md).  
  
 Las variables, asignaciones de variables y restricciones de precedencia también usan expresiones, que pueden incluir comparaciones de cadenas. Para obtener más información sobre las expresiones, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md).  
  
## <a name="processing-during-string-comparison"></a>Procesamiento durante la comparación de cadenas  
 Según los datos y la configuración de la transformación, se puede producir el siguiente procesamiento durante la comparación de datos de cadena:  
  
-   Convertir datos en Unicode. Si los datos de origen no son ya Unicode, los datos se convierten automáticamente en Unicode antes de que se produzca la comparación.  
  
-   Usar la configuración regional para aplicar normas específicas para una región con el fin de interpretar la fecha, la hora, los datos decimales y el orden.  
  
-   Aplicar opciones de comparación a nivel de columna para cambiar la sensibilidad de las comparaciones.  
  
## <a name="converting-string-data-to-unicode"></a>Convertir datos de cadenas en Unicode.  
 Según las operaciones realizadas por la transformación y la configuración de la transformación, los datos de cadena se pueden convertir en el tipo de datos DT_WSTR, que es una representación Unicode de los caracteres de cadenas.  
  
 Los datos de cadena que tienen el tipo de datos DT_STR se convierten a Unicode utilizando la página de códigos de la columna. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite páginas de códigos en el nivel de columna y cada columna se puede convertir mediante una página de códigos diferente.  
  
 En la mayoría de los casos, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede identificar la página de códigos correcta a partir del origen de datos. Por ejemplo, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede establecer una intercalación en los niveles de base de datos y columna. La página de códigos se deriva de una intercalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que puede ser una intercalación de Windows o SQL.  
  
 Si [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona una página de códigos inesperada, o si el paquete obtiene acceso a un origen de datos mediante un proveedor que no ofrece información suficiente para determinar la página de códigos correcta, puede especificar una página de códigos predeterminada en el origen de OLE DB y el destino de OLE DB. Las páginas de códigos predeterminadas se usan en lugar de las páginas de códigos que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los archivos no tienen páginas de códigos. En lugar de ello, los administradores de conexión de archivos planos y de varios archivos planos que usan un paquete para conectarse a los datos de archivos incluyen una propiedad para especificar la página de códigos del archivo. La página de códigos solamente se puede establecer en el nivel de archivo, no en el nivel de columna.  
  
## <a name="setting-locale"></a>Establecer la configuración regional  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no usa la página de códigos para inferir reglas específicas de la configuración regional para ordenar los datos o interpretar los datos de fecha, hora y decimales. En su lugar, la transformación lee la configuración regional fijada por la propiedad LocaleId en el componente de flujo de datos, tarea Flujo de datos, contenedor o paquete. De manera predeterminada, la configuración regional de una transformación es heredada de su tarea Flujo de datos, que a su vez la hereda del paquete. Si la tarea Flujo de datos está en un contenedor como el contenedor de bucles For, hereda su configuración regional del contenedor.  
  
 También puede especificar una configuración regional para un administrador de conexiones de archivos planos y un administrador de conexiones de varios archivos planos.  
  
## <a name="setting-comparison-options"></a>Establecer las opciones de comparación  
 La configuración regional proporciona las reglas básicas para comparar los datos de cadenas. Por ejemplo, la configuración regional especifica la posición de ordenación para cada letra del alfabeto. Sin embargo, estas reglas pueden no ser suficientes para las comparaciones realizadas por algunas transformaciones, y [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite un conjunto de opciones de comparación avanzada que van más allá de las reglas de comparación de una configuración regional. Estas opciones de comparación se establecen en el nivel de columna. Por ejemplo, una de las opciones de comparación le permite omitir los caracteres sin espacio. El efecto de esta opción es omitir los signos diacríticos, tales como los acentos, lo que hace que "a" y "á" resulten idénticas en una comparación.  
  
 La siguiente tabla describe las opciones de comparación y un estilo de ordenación.  
  
|Opción de comparación|Descripción|  
|-----------------------|-----------------|  
|Omitir mayúsculas y minúsculas|Especifica si la comparación distingue entre mayúsculas y minúsculas. Si se establece esta opción, la comparación de las cadenas omite la distinción entre mayúsculas y minúsculas. Por ejemplo, "ABC" se interpreta igual que "abc".|  
|Omitir tipo de kana|Especifica si la comparación distingue entre los dos tipos de caracteres kana japoneses: hiragana y katakana. Si se establece esta opción, la comparación de las cadenas omite los tipos de caracteres kana.|  
|Omitir ancho de caracteres|Especifica si la comparación distingue entre un carácter de un solo byte y el mismo carácter cuando se representa con un carácter de doble byte. Si se establece esta opción, la comparación de las cadenas trata las representaciones de un solo byte y de doble byte del mismo carácter como idénticas.|  
|Omitir caracteres sin espacio|Especifica si la comparación distingue entre caracteres con espacio y signos diacríticos. Si se establece esta opción, la comparación omite los signos diacríticos. Por ejemplo, "å" se considera igual que "a".|  
|Omitir símbolos|Especifica si la comparación distingue entre caracteres que representan letras y los símbolos tales como espacios en blanco, puntuación, símbolos de moneda y símbolos matemáticos. Si se establece esta opción, la comparación de las cadenas omite los símbolos. Por ejemplo, " Nueva York" pasa a ser lo mismo que "Nueva York" y "*ABC" es idéntico a "ABC"'.|  
|Ordenar signos de puntuación como símbolos|Especifica si la comparación ordena todos los símbolos de puntuación, salvo guión y apóstrofo, antes de los caracteres alfanuméricos. Por ejemplo, si se establece esta opción, ".ABC" queda en el orden antes de "ABC".|  
  
 Las transformaciones Ordenar, Agregado, Agrupación aproximada y Búsqueda aproximada incluyen estas opciones para comparar datos.  
  
 La marca de comparación **FullySensitive** aparece en el cuadro de diálogo del **Editor avanzado** de las transformaciones Agrupación aproximada y Búsqueda aproximada. Si se selecciona la marca de comparación **FullySensitive** , esto significa que se aplican todas las opciones de comparación.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de Integration Services](integration-services-data-types.md)   
 [Análisis rápido](../fast-parse.md)   
 [Análisis estándar](../standard-parse.md)  
  
  
