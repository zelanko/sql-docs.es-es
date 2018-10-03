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
manager: craigg
ms.openlocfilehash: 98ff605c2fb701f2451e3df4ba2068da6729ff86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845293"
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
