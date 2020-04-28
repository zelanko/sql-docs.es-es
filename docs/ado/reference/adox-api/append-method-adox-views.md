---
title: Append (método) (vistas ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637932fed7effb87705b3aa195578cfd506e1454
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967154"
---
# <a name="append-method-adox-views"></a>Append (método) (vistas ADOX)
Crea un nuevo objeto de [vista](../../../ado/reference/adox-api/view-object-adox.md) y lo anexa a la colección de [vistas](../../../ado/reference/adox-api/views-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Valor de **cadena** que especifica el nombre de la vista que se va a crear.  
  
 *Comando*  
 Objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO que representa la vista que se va a crear.  
  
## <a name="remarks"></a>Observaciones  
 Crea una nueva vista en el origen de datos con el nombre y los atributos especificados en el objeto de **comando** .  
  
 Si el texto del comando que especifica el usuario representa un procedimiento en lugar de una vista, el comportamiento depende del proveedor. Se producirá un error en **Append** si el proveedor no admite comandos persistentes.  
  
> [!NOTE]
>  Al usar el proveedor de OLE DB para Microsoft Jet, el método **Append** de la colección **views** le permitirá especificar un **procedimiento** en lugar de una **vista** en el parámetro de *comando* . El **procedimiento** se agregará al origen de datos y se agregará a la colección **views** . Después del **método Append**, si se actualizan las colecciones **Procedures** y **views** , el **procedimiento** ya no estará en la colección **views** y aparecerá en la colección **Procedures** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Append de vistas (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
