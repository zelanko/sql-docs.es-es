---
title: Los espacios de nombres | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db90ecbc083a887a9845542b73e50bae6bf61e1e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534743"
---
# <a name="namespaces"></a>Espacios de nombres
El formato de persistencia de XML en ADO utiliza los siguientes espacios de nombres de cuatro.  
  
## <a name="remarks"></a>Comentarios  
 El formato de persistencia de XML en ADO utiliza los siguientes espacios de nombres de cuatro.  
  
|Prefijo|Descripción|  
|------------|-----------------|  
|s|Hace referencia al espacio de nombres "XML-Data" que contiene los elementos y atributos que definen el esquema del conjunto de registros actual.|  
|DT|Hace referencia a la especificación de las definiciones de tipo de datos.|  
|rs|Hace referencia al espacio de nombres que contienen elementos y atributos específicos de las propiedades del conjunto de registros ADO y atributos.|  
|z|Hace referencia al esquema del conjunto de filas actual.|  
  
 Un cliente no debe agregar sus propias etiquetas a estos espacios de nombres, tal como se define mediante la especificación. Por ejemplo, un cliente no debe definir un espacio de nombres como "urn: schemas-microsoft-Rowset" y, a continuación, escribir algo como "rs: MiEtiqueta". Para obtener más información acerca de los espacios de nombres, vea el [W3C recomendación de Namespaces en XML](https://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  El identificador de la etiqueta de esquema debe ser "RowsetSchema" y el espacio de nombres utilizado para hacer referencia al esquema del conjunto de filas actual debe apuntar a "#RowsetSchema."  
  
 Tenga en cuenta que el prefijo del espacio de nombres, la parte entre los dos puntos y el signo igual: es arbitrario.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 El usuario puede definir este puede ser cualquier nombre siempre que este nombre se usa de forma coherente en todo el documento XML. ADO siempre escribe "s", "rs", "dt" y "z", pero estos nombres de prefijo no están codificados en el componente de carga.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
