---
description: Create (método, ADOX)
title: Create (método) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 588f73fcd2ced95be3cd7f8586faed864b38f8ad
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984846"
---
# <a name="create-method-adox"></a>Create (método, ADOX)
Crea un nuevo catálogo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Property*  
 Valor de **cadena** que se usa para conectar con el origen de datos.  
  
## <a name="remarks"></a>Observaciones  
 El método **Create** crea y abre una nueva [conexión](../ado-api/connection-object-ado.md) ado con el origen de datos especificado en *connectstring*. Si se realiza correctamente, el nuevo objeto de **conexión** se asigna a la propiedad [ActiveConnection](./activeconnection-property-adox.md) .  
  
 Se producirá un error si el proveedor no admite la creación de nuevos catálogos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Create (VB)](./create-method-example-vb.md)   
 [ActiveConnection (propiedad, ADOX)](./activeconnection-property-adox.md)