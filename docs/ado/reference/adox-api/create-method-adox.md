---
title: "Create (método) (ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords: Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb1e3dfcf4152060c5828133444ec72ce0994249
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="create-method-adox"></a>Create (método) (ADOX)
Crea un nuevo catálogo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectString*  
 A **cadena** valor utilizado para conectarse al origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 El **crear** método crea y abre un nuevo ADO [conexión](../../../ado/reference/ado-api/connection-object-ado.md) al origen de datos especificado en *ConnectString*. Si se realiza correctamente, el nuevo **conexión** objeto está asignado a la [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propiedad.  
  
 Se producirá un error si el proveedor no admite la creación de nuevos catálogos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear el ejemplo del método (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection (propiedad, ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
