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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967306"
---
# <a name="append-method-adox-indexes"></a>Append (método) (índices ADOX)
Agrega un nuevo objeto [index](../../../ado/reference/adox-api/index-object-adox.md) a la colección [Indexes](../../../ado/reference/adox-api/indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Ajustar*  
 Objeto de **Índice** que se va a anexar o nombre del índice que se va a crear y anexar.  
  
 *Columnas*  
 Opcional. Valor **Variant** que especifica los nombres de las columnas que se van a indizar. El parámetro *Columns* corresponde a los valores de la propiedad [Name](../../../ado/reference/adox-api/name-property-adox.md) de un objeto de [columna](../../../ado/reference/adox-api/column-object-adox.md) u objetos.  
  
## <a name="remarks"></a>Observaciones  
 El parámetro *Columns* puede tomar el nombre de una columna o una matriz de nombres de columna.  
  
 Se producirá un error si el proveedor no admite la creación de índices.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Append de índices (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
