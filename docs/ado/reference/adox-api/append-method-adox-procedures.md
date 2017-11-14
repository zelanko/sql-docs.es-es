---
title: "Append (método) (procedimientos ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 679f7691a8f93026ce1f6a68ea232d01818e6dc9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentarios  
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

