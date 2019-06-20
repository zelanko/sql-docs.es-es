---
title: Item (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords:
- Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6be26e9c174c1911a0c2c7210552c8e8a0e44a2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697567"
---
# <a name="item-property-ado"></a>Propiedad Item (ADO)
Indica a un miembro específico de una colección, por nombre o número ordinal.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve una referencia de objeto.  
  
## <a name="parameters"></a>Parámetros  
 *Index*  
 Un **Variant** expresión que se evalúa como el nombre o el número ordinal de un objeto en una colección.  
  
## <a name="remarks"></a>Comentarios  
 Use la **elemento** propiedad para devolver un objeto específico en una colección. Si **elemento** no se encuentra un objeto en la colección correspondiente a la *índice* argumento, que se produce un error. Además, algunas colecciones no admiten objetos con nombre; para estas colecciones, debe utilizar las referencias de número ordinal.  
  
 El **elemento** es la propiedad predeterminada para todas las colecciones; por lo tanto, las siguientes formas de sintaxis son intercambiables:  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Colección Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de niveles (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Colección de posiciones (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad Item (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Ejemplo de la propiedad de elemento (VC ++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
