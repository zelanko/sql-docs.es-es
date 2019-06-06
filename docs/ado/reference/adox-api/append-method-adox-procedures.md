---
title: Append (método) (procedimientos ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1c379826b16ef805abfedb0467d3385010ca1b99
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708585"
---
# <a name="append-method-adox-procedures"></a>Append (método) (procedimientos ADOX)
Agrega un nuevo [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md) de objeto para el [procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Name*  
 Un **cadena** valor que especifica el nombre del procedimiento para crear y anexar.  
  
 *Command*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa el procedimiento para crear y anexar.  
  
## <a name="remarks"></a>Comentarios  
 Crea un nuevo procedimiento en el origen de datos con el nombre y los atributos especificados en el **comando** objeto.  
  
 Si el texto del comando que especifica el usuario representa una vista en lugar de un procedimiento, el comportamiento depende del proveedor que se utiliza. **Anexar** se producirá un error si el proveedor no admite comandos persistentes.  
  
> [!NOTE]
>  Cuando se usa el proveedor OLE DB para Microsoft Jet, la **procedimientos** colección **Append** método le permitirá especificar una **vista** en lugar de un  **Procedimiento** en el *comando* parámetro. El **vista** se agregará al origen de datos y se agregará a la **procedimientos** colección. Después de la **Append**, si la **procedimientos** y **vistas** se actualizan las colecciones, el **vista** dejará de estar en el **Procedimientos** colección y aparecerá en el **vistas** colección.  
  
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
