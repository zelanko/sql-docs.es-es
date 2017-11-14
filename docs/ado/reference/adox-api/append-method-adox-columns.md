---
title: "Append (método) (columnas ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c6c9323dbc1e3c69445dc09ad06373856fb67bc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-columns"></a>Append (método) (columnas ADOX)
Agrega un nuevo [columna](../../../ado/reference/adox-api/column-object-adox.md) el objeto a la [columnas](../../../ado/reference/adox-api/columns-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Columna*  
 El **columna** objeto que se anexará o el nombre de la columna para crear y anexar.  
  
 *Tipo*  
 Opcional. A **largo** valor que especifica el tipo de datos de la columna. El *tipo* parámetro corresponde a la [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propiedad de un **columna** objeto.  
  
 *DefinedSize*  
 Opcional. A **largo** valor que especifica el tamaño de la columna. El *DefinedSize* parámetro corresponde a la [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) propiedad de un **columna** objeto.  
  
> [!NOTE]
>  Se producirá un error al anexar un **columna** a la **columnas** colección de un [índice](../../../ado/reference/adox-api/index-object-adox.md) si la **columna** no existe en un [Tabla](../../../ado/reference/adox-api/table-object-adox.md) ya que se anexa a la [tablas](../../../ado/reference/adox-api/tables-collection-adox.md) colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Las tablas y columnas anexar métodos, ejemplo de la propiedad de nombre (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Ejemplo de propiedad ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (ADOX procedimientos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)

