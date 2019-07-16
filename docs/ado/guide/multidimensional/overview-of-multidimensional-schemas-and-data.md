---
title: Información general de esquemas y datos multidimensionales | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e4681bb9e1fd1028ee1ddc2bd7f72efc03fb6c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923187"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>Información general de esquemas y datos multidimensionales
## <a name="understanding-multidimensional-schemas"></a>Esquemas multidimensionales  
 El objeto de metadatos central en ADO MD es el *cubo*, que consta de un conjunto estructurado de dimensiones relacionadas, jerarquías, niveles y miembros.  
  
 Un *dimensión* es una categoría independiente de los datos de la base de datos multidimensional, derivado de las entidades empresariales. Normalmente, una dimensión contiene los elementos que se usará como criterio de consulta para las medidas de la base de datos.  
  
 Un *jerarquía* es una ruta de acceso de agregación de una dimensión. Una dimensión puede tener varios niveles de granularidad, con relaciones de elementos primarios y secundarios. Una jerarquía define cómo se relacionan estos niveles.  
  
 Un *nivel* es un paso de agregación de una jerarquía. Para las dimensiones con varias capas de información, cada capa es un nivel.  
  
 Un *miembro* es un elemento de datos en una dimensión. Normalmente, crea un título o describir una medida de la base de datos con los miembros.  
  
 Los cubos se representan mediante [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objetos de ADO MD. Las dimensiones, jerarquías, niveles y miembros también se representan mediante sus objetos ADO MD correspondientes: [Dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md), y [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md).  
  
### <a name="dimensions"></a>Dimensions  
 Las dimensiones de un cubo dependen de sus entidades empresariales y los tipos de datos que se quieran modelar en la base de datos. Normalmente, cada dimensión es un punto de entrada independiente o un mecanismo para seleccionar datos.  
  
 Por ejemplo, un cubo que contiene los datos de ventas tiene las cinco dimensiones siguientes: Empleado de ventas, geografía, tiempo, productos y medidas. La dimensión de medidas contiene valores de datos de ventas reales, mientras que las otras dimensiones representan formas de clasificar y agrupar los valores de datos de ventas.  
  
 La dimensión Geography tiene el siguiente conjunto de miembros:  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>Jerarquías  
 Las jerarquías definen las formas en el que los niveles de una dimensión pueden ser "acumular" o agrupados. Una dimensión puede tener más de una jerarquía. Existe una jerarquía natural en la dimensión Geography:  
  
### <a name="levels"></a>Niveles  
 En la dimensión Geography de ejemplo se ilustran en la figura anterior, cada cuadro representa un nivel de la jerarquía.  
  
 Cada nivel tiene un conjunto de miembros, como sigue:  
  
-   El mundo `= {All}`  
  
-   Continentes `= {North America, Europe}`  
  
-   Países `= {Canada, USA, UK, Germany}`  
  
-   Regiones `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   Ciudades `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>Miembros  
 Los miembros del nivel de hoja de una jerarquía no tienen elementos secundarios y los miembros del nivel raíz no tienen ningún elemento primario. Todos los demás miembros tienen al menos un elemento primario y al menos un elemento secundario. Por ejemplo, un recorrido del árbol de jerarquía de la dimensión Geography parcial da como resultado las siguientes relaciones de elementos primarios y secundarios:  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 Los miembros se pueden consolidar a lo largo de una o varias jerarquías por dimensión. Considere la posibilidad de una dimensión de tiempo donde desde el nivel de días de acumulación para el nivel de año de dos formas:  
  
 Este ejemplo también muestra otra característica: Algunos miembros del nivel semana de la jerarquía de la semana del año no aparecen en cualquier nivel de la jerarquía de trimestre del año. Por lo tanto, no necesita incluir a todos los miembros de una dimensión de una jerarquía.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Programar con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usar ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Trabajo con datos multidimensionales](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
