---
title: "Append (método) (claves ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eead7a8702c927e13b11cb75f2a5a3881a2065fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="append-method-adox-keys"></a>Append (método) (claves ADOX)
Agrega un nuevo [clave](../../../ado/reference/adox-api/key-object-adox.md) el objeto a la [claves](../../../ado/reference/adox-api/keys-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Key*  
 El **clave** objeto que se anexará o el nombre de la clave para crear y anexar.  
  
 *KeyType*  
 Opcional. A **largo** valor que especifica el tipo de clave. El *clave* parámetro corresponde a la [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propiedad de un **clave** objeto.  
  
 *Columna*  
 Opcional. A **cadena** valor que especifica el nombre de la columna que se va a indizar. El *columnas* parámetro corresponde al valor de la [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad de un [columna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
 *RelatedTable*  
 Opcional. A **cadena** valor que especifica el nombre de la tabla relacionada. El *RelatedTable* parámetro corresponde al valor de la **nombre** propiedad de un [tabla](../../../ado/reference/adox-api/table-object-adox.md) objeto.  
  
 *RelatedColumn*  
 Opcional. A **cadena** valor que especifica el nombre de la columna relacionada para una clave externa. El *RelatedColumn* parámetro corresponde al valor de la **nombre** propiedad de un [columna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 El *columnas* parámetro puede tomar el nombre de una columna o una matriz de nombres de columna.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar de teclas de método, tipo de clave, RelatedColumn, RelatedTable y ejemplo de las propiedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (ADOX procedimientos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
