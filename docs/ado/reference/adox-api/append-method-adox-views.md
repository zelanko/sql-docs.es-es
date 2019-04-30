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
manager: craigg
ms.openlocfilehash: 584c3d0144197425b307f2d4a04bd8a09f27a36c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184218"
---
# <a name="append-method-adox-views"></a>Append (método) (vistas ADOX)
Crea un nuevo [vista](../../../ado/reference/adox-api/view-object-adox.md) objeto y lo anexa a la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Name*  
 Un **cadena** valor que especifica el nombre de la vista para crear.  
  
 *Command*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa la vista para crear.  
  
## <a name="remarks"></a>Comentarios  
 Crea una nueva vista del origen de datos con el nombre y los atributos especificados en el **comando** objeto.  
  
 Si el texto del comando que especifica el usuario representa un procedimiento en lugar de una vista, el comportamiento depende del proveedor. **Anexar** se producirá un error si el proveedor no admite comandos persistentes.  
  
> [!NOTE]
>  Cuando se usa el proveedor OLE DB para Microsoft Jet, la **vistas** colección **Append** método le permitirá especificar una **procedimiento** en lugar de un **vista**  en el *comando* parámetro. El **procedimiento** se agregará al origen de datos y se agregará a la **vistas** colección. Después de la **Append**, si la **procedimientos** y **vistas** se actualizan las colecciones, el **procedimiento** dejará de estar en el **Vistas** colección y aparecerá en el **procedimientos** colección.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas de ejemplo de método Append (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (procedimientos ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (usuarios ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
