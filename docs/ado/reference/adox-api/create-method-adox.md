---
title: Crear (método, ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ca88f95882da8e900e7695f81570b46977db9c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183852"
---
# <a name="create-method-adox"></a>Create (método, ADOX)
Crea un nuevo catálogo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectString*  
 Un **cadena** valor usado para conectarse al origen de datos.  
  
## <a name="remarks"></a>Comentarios  
 El **crear** método crea y abre un nuevo ADO [conexión](../../../ado/reference/ado-api/connection-object-ado.md) al origen de datos especificado en *ConnectString*. Si se realiza correctamente, el nuevo **conexión** se asigna a la [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propiedad.  
  
 Se producirá un error si el proveedor no admite la creación de nuevos catálogos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear el ejemplo del método (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection (propiedad, ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
