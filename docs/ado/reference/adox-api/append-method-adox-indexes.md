---
description: Append (método) (índices ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 28e396e85dc68a3d622a173dad440c5dff68dea1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771464"
---
# <a name="append-method-adox-indexes"></a>Append (método) (índices ADOX)
Agrega un nuevo objeto [index](./index-object-adox.md) a la colección [Indexes](./indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Index*  
 Objeto de **Índice** que se va a anexar o nombre del índice que se va a crear y anexar.  
  
 *Columnas*  
 Opcional. Valor **Variant** que especifica los nombres de las columnas que se van a indizar. El parámetro *Columns* corresponde a los valores de la propiedad [Name](./name-property-adox.md) de un objeto de [columna](./column-object-adox.md) u objetos.  
  
## <a name="remarks"></a>Observaciones  
 El parámetro *Columns* puede tomar el nombre de una columna o una matriz de nombres de columna.  
  
 Se producirá un error si el proveedor no admite la creación de índices.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de índices (ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Append de índices (VB)](./indexes-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](./append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](./append-method-adox-groups.md)   
 [Append (método) (claves ADOX)](./append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](./append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](./append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](./append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](./append-method-adox-views.md)