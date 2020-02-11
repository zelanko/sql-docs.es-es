---
title: Append (método) (columnas ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6493157c00e5a71c7c2f085191231bb33bb5279a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967327"
---
# <a name="append-method-adox-columns"></a>Append (método) (columnas ADOX)
Agrega un nuevo objeto de [columna](../../../ado/reference/adox-api/column-object-adox.md) a la colección de [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Columna*  
 Objeto de **columna** que se va a anexar o nombre de la columna que se va a crear y anexar.  
  
 *Tipo*  
 Opcional. Valor **largo** que especifica el tipo de datos de la columna. El parámetro de *tipo* corresponde a la propiedad [Type](../../../ado/reference/adox-api/type-property-column-adox.md) de un objeto **Column** .  
  
 *DefinedSize*  
 Opcional. Valor de **tipo Long** que especifica el tamaño de la columna. El parámetro *DefinedSize* corresponde a la propiedad [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) de un objeto **Column** .  
  
> [!NOTE]
>  Se producirá un error al anexar una **columna** a la colección de **columnas** de un [Índice](../../../ado/reference/adox-api/index-object-adox.md) si la **columna** no existe en una [tabla](../../../ado/reference/adox-api/table-object-adox.md) que ya esté anexada a la colección de [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Name, métodos Append de columnas y tablas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ejemplo de las propiedades de método Append, tipo de clave, RelatedColumn, RelatedTable y UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
