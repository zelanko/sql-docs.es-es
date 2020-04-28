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
ms.openlocfilehash: dd64ba8119db1ecf2d2b621cd202c9f700b53475
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967282"
---
# <a name="append-method-adox-procedures"></a>Append (método) (procedimientos ADOX)
Agrega un nuevo objeto de [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md) a la colección [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Valor de **cadena** que especifica el nombre del procedimiento que se va a crear y anexar.  
  
 *Comando*  
 Objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO que representa el procedimiento que se va a crear y anexar.  
  
## <a name="remarks"></a>Observaciones  
 Crea un nuevo procedimiento en el origen de datos con el nombre y los atributos especificados en el objeto de **comando** .  
  
 Si el texto del comando que especifica el usuario representa una vista en lugar de un procedimiento, el comportamiento depende del proveedor que se está usando. Se producirá un error en **Append** si el proveedor no admite comandos persistentes.  
  
> [!NOTE]
>  Al usar el proveedor de OLE DB para Microsoft Jet, el método **Append** de la colección **Procedures** le permitirá especificar una **vista** en lugar de un **procedimiento** en el parámetro de *comando* . La **vista** se agregará al origen de datos y se agregará a la colección **Procedures** . Después de **anexar**, si se actualizan las colecciones **Procedures** y **views** , la **vista** ya no estará en la colección **Procedures** y aparecerá en la colección **views** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de método Append de procedimientos (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
