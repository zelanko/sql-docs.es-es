---
title: Espacios de nombres | Documentos de Microsoft
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
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d9dd5aab887a7df42fd1f6661c276be6cc73d6a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="namespaces"></a>Espacios de nombres
El formato de persistencia de XML en ADO utiliza los siguientes espacios de nombres de cuatro.  
  
## <a name="remarks"></a>Comentarios  
 El formato de persistencia de XML en ADO utiliza los siguientes espacios de nombres de cuatro.  
  
|Prefijo|Description|  
|------------|-----------------|  
|s|Hace referencia al espacio de nombres "XML-Data" que contiene los elementos y atributos que definen el esquema del conjunto de registros actual.|  
|DT|Hace referencia a la especificación de las definiciones de tipo de datos.|  
|rs|Hace referencia al espacio de nombres que contienen elementos y atributos específicos de propiedades de conjunto de registros ADO y atributos.|  
|z|Hace referencia al esquema del conjunto de filas actual.|  
  
 Un cliente no debe agregar sus propias etiquetas a estos espacios de nombres, tal como se define en la especificación. Por ejemplo, un cliente no debe definir un espacio de nombres como "urn: schemas-microsoft-Rowset" y, a continuación, escribir algo como "rs: MiEtiqueta". Para obtener más información sobre los espacios de nombres, vea la [espacios de nombres de W3C en la recomendación de XML](http://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  El identificador de la etiqueta del esquema debe ser "RowsetSchema" y el espacio de nombres utilizado para hacer referencia al esquema del conjunto de filas actual debe apuntar a "#RowsetSchema".  
  
 Tenga en cuenta que el prefijo del espacio de nombres, la parte situada entre los dos puntos y el signo igual, es arbitrario.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 El usuario puede definir este puede ser cualquier nombre siempre que este nombre se usa de forma coherente en todo el documento XML. ADO siempre escribe "s", "rs", "dt" y "z", pero estos nombres de prefijos no están codificados de forma rígida en el componente de carga.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
