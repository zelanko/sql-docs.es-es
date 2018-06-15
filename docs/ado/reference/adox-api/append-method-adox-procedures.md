---
title: Append (método) (procedimientos ADOX) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc5721f8806481de872d0c3e1de7d47a3720dfa9
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284864"
---
# <a name="append-method-adox-procedures"></a>Append (método) (ADOX procedimientos)
Agrega un nuevo [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md) el objeto a la [procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 A **cadena** valor que especifica el nombre del procedimiento para crear y anexar.  
  
 *Command*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa el procedimiento para crear y anexar.  
  
## <a name="remarks"></a>Notas  
 Crea un nuevo procedimiento en el origen de datos con el nombre y los atributos especificados en el **comando** objeto.  
  
 Si el texto del comando que especifica el usuario representa una vista en lugar de un procedimiento, el comportamiento depende del proveedor que se está usando. **Anexar** se producirá un error si el proveedor no admite comandos persistentes.  
  
> [!NOTE]
>  Cuando se utiliza el proveedor OLE DB para Microsoft Jet, el **procedimientos** colección **anexado** método le permitirá especificar una **vista** en lugar de un  **Procedimiento** en el *comando* parámetro. El **vista** se agregará al origen de datos y se agregará a la **procedimientos** colección. Después de la **anexado**, si la **procedimientos** y **vistas** se actualizan las colecciones, el **vista** ya no estará en el **Procedimientos** colección y se mostrarán en el **vistas** colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos de ejemplo de método Append (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
