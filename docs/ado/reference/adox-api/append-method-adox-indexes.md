---
title: "Append (método) (índices ADOX) | Documentos de Microsoft"
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
f1_keywords: Indexes::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27ddeee201dba9d1381b31023039256d9e587a1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="append-method-adox-indexes"></a>Append (método) (índices ADOX)
Agrega un nuevo [índice](../../../ado/reference/adox-api/index-object-adox.md) el objeto a la [índices](../../../ado/reference/adox-api/indexes-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Index*  
 El **índice** objeto que se anexará o el nombre del índice que se va a crear y anexar.  
  
 *Columnas*  
 Opcional. A **Variant** valor que especifica los nombres de las columnas que se debe indexar. El *columnas* parámetro corresponde a los valores de la [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad de un [columna](../../../ado/reference/adox-api/column-object-adox.md) objeto u objetos.  
  
## <a name="remarks"></a>Comentarios  
 El *columnas* parámetro puede tomar el nombre de una columna o una matriz de nombres de columna.  
  
 Se producirá un error si el proveedor no admite la creación de índices.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Índices de ejemplo de método Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (ADOX procedimientos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
