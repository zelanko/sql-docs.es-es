---
title: Append (método) (índices ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef30faf0fef05c4e86ffb4d2c21781592094c198
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967306"
---
# <a name="append-method-adox-indexes"></a>Append (método) (índices ADOX)
Agrega un nuevo [índice](../../../ado/reference/adox-api/index-object-adox.md) de objeto para el [índices](../../../ado/reference/adox-api/indexes-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Index*  
 El **índice** objeto anexar o el nombre del índice que se va a crear y anexar.  
  
 *Columnas*  
 Opcional. Un **Variant** valor que especifica los nombres de las columnas que se puede indizar. El *columnas* parámetro corresponde a los valores de la [nombre](../../../ado/reference/adox-api/name-property-adox.md) propiedad de un [columna](../../../ado/reference/adox-api/column-object-adox.md) objeto u objetos.  
  
## <a name="remarks"></a>Comentarios  
 El *columnas* parámetro puede tomar el nombre de una columna o una matriz de nombres de columna.  
  
 Se producirá un error si el proveedor no admite la creación de índices.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Los índices de ejemplo de método Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
