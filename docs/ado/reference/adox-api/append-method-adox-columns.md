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
manager: jroth
ms.openlocfilehash: e8ac03231680ecd807234b20ac7b210bc480f2c1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708487"
---
# <a name="append-method-adox-columns"></a>Append (método) (columnas ADOX)
Agrega un nuevo [columna](../../../ado/reference/adox-api/column-object-adox.md) de objeto para el [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Columna*  
 El **columna** objeto anexar o el nombre de la columna para crear y anexar.  
  
 *Tipo*  
 Opcional. Un **largo** valor que especifica el tipo de datos de la columna. El *tipo* parámetro corresponde a la [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propiedad de un **columna** objeto.  
  
 *DefinedSize*  
 Opcional. Un **largo** valor que especifica el tamaño de la columna. El *DefinedSize* parámetro corresponde a la [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) propiedad de un **columna** objeto.  
  
> [!NOTE]
>  Se producirá un error al anexar un **columna** a la **columnas** colección de un [índice](../../../ado/reference/adox-api/index-object-adox.md) si el **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) ya que se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de nombre (VB), métodos Append columnas y tablas](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Append de claves, método, tipo de clave, RelatedColumn, RelatedTable y UpdateRule propiedades (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
