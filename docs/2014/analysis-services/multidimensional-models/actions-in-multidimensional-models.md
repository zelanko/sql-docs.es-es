---
title: Acciones en modelos multidimensionales | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 825343c58feeb7ffb217a8b1c8c53d8f81ae7441
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077503"
---
# <a name="actions-in-multidimensional-models"></a>Acciones en modelos multidimensionales
  Una acción es una operación iniciada por el usuario final en un cubo seleccionado o en una parte de un cubo. La operación puede iniciar una aplicación con el elemento seleccionado como parámetro o recuperar información acerca del elemento seleccionado. Para más información sobre las acciones, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](actions-analysis-services-multidimensional-data.md).  
  
 Use la pestaña **Acciones** del Diseñador de cubos para generar acciones para un cubo. Especifique lo siguiente:  
  
 **Nombre**  
 Seleccione un nombre que identifique la acción.  
  
 **Destino de la acción**  
 Seleccione el objeto al que se adjunta la acción. Normalmente, en aplicaciones cliente, la acción se muestra cuando los usuarios finales seleccionan el objeto de destino; no obstante, la aplicación cliente determina la operación del usuario final que muestra las acciones. En **Tipo de destino**, seleccione entre los siguientes objetos:  
  
-   Miembros del atributo  
  
-   Celdas  
  
-   Cube  
  
-   miembros de dimensión  
  
-   Hierarchy  
  
-   Miembros de la jerarquía  
  
-   Nivel  
  
-   Miembros del nivel  
  
 Después de seleccionar el tipo de objeto de destino, en **Objeto de destino**, seleccione el objeto de cubo del tipo designado.  
  
 **Condición (opcional)**  
 Especifique una expresión opcional de Expresiones multidimensionales (MDX) que se resuelva en un valor booleano. Si el valor es `True`, la acción se realiza en el destino especificado. Si el valor es `False`, la acción no se realiza.  
  
 **Contenido de la acción**  
 Seleccione el tipo de acción. La siguiente tabla contiene los tipos disponibles.  
  
|Tipo|Descripción|  
|----------|-----------------|  
|Conjunto de datos|Recupera un conjunto de datos.|  
|Propietario|Ejecuta una operación con una interfaz que no aparece en esta tabla.|  
|Conjunto de filas|Recupera un conjunto de filas.|  
|.|Ejecuta un comando OLE DB.|  
|URL|Muestra una página variable en un explorador de Internet.|  
  
 En **Expresión de acción**, especifique los parámetros que se pasan cuando se ejecuta la acción. La sintaxis se debe evaluar como una cadena, y debe incluirse una expresión escrita en MDX. Por ejemplo, la expresión MDX puede indicar una parte del cubo incluida en la sintaxis. Las expresiones MDX se evalúan antes de pasar los parámetros. Además, el Generador MDX ayuda a generar expresiones MDX.  
  
 **Propiedades adicionales**  
 Seleccione la propiedad. En la siguiente tabla se resumen las propiedades disponibles.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**Invocación**|Especifica cómo se ejecuta la acción. Interactiva, que es la opción predeterminada, especifica que la acción se ejecuta cuando un usuario tiene acceso a un objeto. Los valores posibles son:<br /><br /> Batch<br /><br /> Interactive<br /><br /> Al abrir|  
|**Aplicación**|Describe la aplicación de la acción.|  
|**Descripción**|Describe la acción.|  
|**Caption**|Proporciona un título que se muestra para la acción. Si el título es MDX, especifique `True` para **título es MDX**.|  
|**El título es MDX**|Especifique `True` si el título es MDX o `False` si no lo es.|  
  
> [!NOTE]  
>  Debe usar Lenguaje de scripting de Analysis Services (ASSL) u Objetos de administración de análisis (AMO) para definir tipos de acciones de la línea de comandos y HTML. Para más información, vea [Elemento Action &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/action-element-assl), [Elemento Type &#40;Action&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-action-assl) y [Programar objetos avanzados OLAP en AMO](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-advanced-objects).  
  
## <a name="creating-a-reporting-action"></a>Crear una acción de informe  
 El servidor de informes responde a las solicitudes basadas en URL para los informes. Para crear una acción de informe, en el menú **Cubo** , haga clic en **Nueva acción de informe**. Las siguientes opciones son específicas de una acción de informe.  
  
 **Servidor de informes**  
 Las propiedades descritas en la siguiente tabla se especifican para el servidor de informes.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|**Nombre del servidor**|Nombre del equipo en el que se ejecuta el servidor de informes.|  
|**Ruta de acceso del servidor**|La ruta de acceso expuesta por un servidor de informes.|  
|**Formato de informe**|HTML5, HTML3, Excel o PDF.|  
  
 **Parámetros (opcional)**  
 Los parámetros se envían al servidor como parte de la cadena URL cuando se crea la acción. Incluyen **Nombre de parámetro** y **Valor de parámetro**, que es una expresión MDX.  
  
 La URL del servidor de informes se genera de la manera siguiente:  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 Por ejemplo:  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>Crear una acción de obtención de detalles  
 Una acción de obtención de detalles se define mediante una acción de conjunto de filas, que se devuelve a la aplicación cliente como una instrucción de obtención de detalles. El destino de la acción es un miembro de un grupo de medida. Para crear una acción de obtención de detalles, en el menú **Cubo** , haga clic en **Nueva acción de obtención de detalles**. Las siguientes opciones son específicas de una acción de obtención de detalles.  
  
 **Columnas de obtención de detalles**  
 Seleccione una o más dimensiones y, para cada dimensión, las columnas de obtención de detalles devueltas a la aplicación cliente por la acción.  
  
## <a name="see-also"></a>Consulte también  
 [Cubos en modelos multidimensionales](cubes-in-multidimensional-models.md)  
  
  
