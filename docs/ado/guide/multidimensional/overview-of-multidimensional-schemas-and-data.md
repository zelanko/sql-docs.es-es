---
title: "Información general de esquemas y datos multidimensionales | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf3e8d6bebd5860df9f52236eecf4d1f287a8f9d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Información general de esquemas y datos multidimensionales
## <a name="understanding-multidimensional-schemas"></a>Esquemas multidimensionales  
 El objeto de metadatos central en ADO MD es el *cubo*, que consta de un conjunto estructurado de dimensiones relacionadas, jerarquías, niveles y miembros.  
  
 A *dimensión* es una categoría independiente de datos de la base de datos multidimensional, derivada de las entidades empresariales. Normalmente, una dimensión contiene elementos que se usará como criterio de consulta para las medidas de la base de datos.  
  
 A *jerarquía* es una ruta de agregación de una dimensión. Una dimensión puede tener varios niveles de granularidad, que tienen relaciones de elementos primarios y secundarios. Una jerarquía define cómo se relacionan estos niveles.  
  
 A *nivel* es un paso de agregación de una jerarquía. Para las dimensiones con varias capas de información, cada capa es un nivel.  
  
 A *miembro* es un elemento de datos en una dimensión. Normalmente, se crea un título o describir una medida de la base de datos usando a los miembros.  
  
 Los cubos se representan mediante [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objetos de ADO MD. Dimensiones, jerarquías, niveles y miembros se representan también mediante sus objetos ADO MD correspondientes: [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md), y [ Miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensions  
 Las dimensiones de un cubo dependen el entidades empresariales y los tipos de datos que se modela en la base de datos. Normalmente, cada dimensión es un punto de entrada independiente o un mecanismo para seleccionar los datos.  
  
 Por ejemplo, un cubo que contiene datos de ventas tiene las cinco dimensiones siguientes: vendedor, geografía, hora, productos y medidas. La dimensión de medidas contiene valores de datos de ventas reales, mientras que las otras dimensiones representan formas de clasificar y agrupar los valores de datos de ventas.  
  
 La dimensión Geography tiene el siguiente conjunto de miembros:  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>Jerarquías  
 Las jerarquías definen la forma en la que se pueden "acumular" o agrupan los niveles de una dimensión. Una dimensión puede tener más de una jerarquía. Existe una jerarquía natural en la dimensión Geography:  
  
### <a name="levels"></a>Niveles  
 En la dimensión Geography de ejemplo se ilustran en la figura anterior, cada cuadro representa un nivel de la jerarquía.  
  
 Cada nivel tiene un conjunto de miembros, como se indica a continuación:  
  
-   Todo el mundo`= {All}`  
  
-   Continentes`= {North America, Europe}`  
  
-   Países`= {Canada, USA, UK, Germany}`  
  
-   Regiones`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Ciudades`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Miembros  
 Los miembros del nivel de hoja de una jerarquía no tienen elementos secundarios y los miembros del nivel raíz tienen ningún elemento primario. Todos los demás miembros tienen al menos un elemento primario y al menos un elemento secundario. Por ejemplo, un recorrido transversal parcial del árbol de jerarquía de la dimensión Geography genera las relaciones de elementos primarios y secundarios siguientes:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Los miembros se pueden consolidar en una o más jerarquías por dimensión. Considere la posibilidad de una dimensión de tiempo que hay dos formas para acumular en el nivel de año desde el nivel de días:  
  
 Este ejemplo ilustra también otra característica: algunos miembros del nivel semana de la jerarquía de la semana del año no aparecen en cualquier nivel de la jerarquía de trimestre del año. Por lo tanto, una jerarquía no necesita incluir a todos los miembros de una dimensión.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos de ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usar ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Trabajar con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)

