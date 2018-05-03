---
title: Datos de Microsoft para dar forma al servicio para OLE DB (proveedor de servicios de ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 615976f4de2a27c9ddb82cf2263cfcdfa0fc9723
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>Datos de Microsoft para dar forma al servicio para información general acerca OLE DB
> [!IMPORTANT]
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, las aplicaciones deben utilizar XML.

 El servicio de forma de datos de Microsoft para el proveedor de servicio de OLE DB admite la construcción de jerárquica (forma) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos desde un proveedor de datos.

## <a name="provider-keyword"></a>Palabra clave del proveedor
 Para invocar el servicio de forma de datos para OLE DB, especifique la siguiente palabra clave y valor en la cadena de conexión.

```
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca este proveedor de servicios, se agregan las siguientes propiedades dinámicas a la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de la[conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.

|Nombre de la propiedad dinámica|Description|
|---------------------------|-----------------|
|**Nombres de cambio de forma única**|Indica si **Recordset** objetos con valores duplicados para sus **cambiar la forma de nombre** propiedades están permitidas. Si esta propiedad dinámica es **True** y una nueva **Recordset** se crea con el mismo nombre de cambio de forma especificado por el usuario que existente **conjunto de registros**, a continuación, el nuevo  **Conjunto de registros** nombre para modificar la forma del objeto se modifica para que sea único. Si esta propiedad es **False** y una nueva **Recordset** se crea con el mismo nombre de cambio de forma especificado por el usuario que existente **Recordset**, ambos **conjunto de registros**  objetos tendrán el mismo nombre de cambio de forma. Por lo tanto, ninguna de ellas **Recordset** puede cambiarse siempre que existan dos conjuntos de registros.<br /><br /> El valor predeterminado de la propiedad es **False**.|
|**Proveedor de datos**|Indica el nombre del proveedor que suministrará las filas para dar forma. Este valor puede ser Ninguno si no se utilizará un proveedor para suministrar filas.|

 También puede establecer propiedades dinámicas escritura especificando sus nombres como palabras clave en la cadena de conexión. Por ejemplo, en Microsoft Visual Basic, establezca la **proveedor de datos** propiedad dinámica en "MSDASQL" al especificar:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 También puede establecer o recuperar una propiedad dinámica al especificar su nombre como el índice de la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) propiedad. Por ejemplo, en el ejemplo de código siguiente se obtiene y se imprime el valor actual de la **proveedor de datos** propiedad dinámica, a continuación, establece un nuevo valor si cn. DataProvider se ha establecido en "MSDataShape" (directa o indirectamente a través de la cadena de conexión) y no se ha abierto la conexión:

```
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  La propiedad dinámica, **proveedor de datos**, también se puede establecer solo en una no está abierto y **conexión** objeto. Una vez que se abre la conexión, el **proveedor de datos** propiedad pasa a ser de solo lectura.

 Para obtener más información sobre la forma de datos, vea [dar forma a datos](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Vea también
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
