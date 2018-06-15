---
title: Elemento de propiedad (conjunto de celdas de ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64de692b36cd2abda06402e5c0d55c250b9632f5
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284084"
---
# <a name="item-property-ado-md-cellset"></a>Propiedad Item (conjunto de celdas de ADO MD)
Recupera una celda de un [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) utilizando sus coordenadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parámetros  
 *Posiciones*  
 A **VariantArray** de valores que especifican inequívocamente una celda. *Posiciones* puede ser uno de los siguientes:  
  
-   Una matriz de números de posición  
  
-   Una matriz de nombres de miembro  
  
-   La posición ordinal  
  
## <a name="remarks"></a>Notas  
 Use la **elemento** propiedad para devolver un [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto dentro de un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto. Si el **elemento** propiedad no puede encontrar la celda correspondiente a la *posiciones* argumento, que se produce un error.  
  
 El **elemento** es la propiedad predeterminada para el **Cellset** objeto. Las siguientes formas de sintaxis son intercambiables:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Notas  
 El *posiciones* especifica el argumento de la celda que se devuelven. Puede especificar la celda por su posición ordinal o por la posición de cada eje. Al especificar la celda por la posición de cada eje, puede especificar el valor numérico de la posición o los nombres de los miembros de cada posición.  
  
 La posición ordinal es un número que identifica de forma única una celda dentro de la **Cellset**. Conceptualmente, las celdas se numeran en un **Cellset** como si la **Cellset** eran un *p*-matriz unidimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila. A continuación se muestra la fórmula para calcular el número ordinal de una celda:  
  
 Si los nombres de miembro se pasan como cadenas a **elemento**, los miembros deben especificarse en orden creciente de los identificadores de eje numérico. Dentro de un eje, los miembros deben especificarse en orden creciente de las dimensiones anidadas, es decir, miembro de la dimensión más externa ocurra primero, seguido por los miembros de las dimensiones interiores. Cada dimensión debe representarse mediante una cadena distinta, y la lista de cadenas de miembro debe ir separada por comas.  
  
> [!NOTE]
>  Recuperación de celdas por nombre de miembro no se admite el proveedor de datos. Consulte la documentación de su proveedor para obtener más información.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
