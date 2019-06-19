---
title: Servicio de OLE DB (proveedor de servicios de ADO) de la forma de datos de Microsoft | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7741cc84b27991cc0831e5e28f397f46d22020a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701214"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>OLE DB Introducción al servicio para la forma de datos de Microsoft
> [!IMPORTANT]
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, las aplicaciones deben usar XML.

 El servicio de forma de datos de Microsoft para el proveedor de servicios OLE DB admite la construcción de jerárquica (forma) [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos desde un proveedor de datos.

## <a name="provider-keyword"></a>Palabra clave del proveedor
 Para invocar el servicio de forma de datos para OLE DB, especifique la siguiente palabra clave y valor en la cadena de conexión.

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>Propiedades dinámicas
 Cuando se invoca este proveedor de servicios, se agregan las siguientes propiedades dinámicas a la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de la[conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.

|Nombre de propiedad dinámica|Descripción|
|---------------------------|-----------------|
|**Nombres de remodelación único**|Indica si **Recordset** objetos con valores duplicados para sus **Reshape Name** se permiten propiedades. Si esta propiedad dinámica es **True** y un nuevo **Recordset** se crea con el mismo nombre de modificar la forma especificada por el usuario que una existente **Recordset**, a continuación, el nuevo  **Conjunto de registros** reshape el nombre del objeto se modifica para que sea único. Si esta propiedad es **False** y un nuevo **Recordset** se crea con el mismo nombre de modificar la forma especificada por el usuario que la existente **Recordset**, ambos **conjunto de registros**  objetos tendrán el mismo nombre de remodelación. Por lo tanto, ninguna de ellas **Recordset** puede cambiarse siempre que existan ambos conjuntos de registros.<br /><br /> El valor predeterminado de la propiedad es **False**.|
|**Proveedor de datos**|Indica el nombre del proveedor que suministrará las filas que se va a dar. Este valor puede ser Ninguno si no se utilizará un proveedor para proporcionar las filas.|

 También puede establecer propiedades dinámicas grabables especificando sus nombres como palabras clave en la cadena de conexión. Por ejemplo, en Microsoft Visual Basic, establezca la **proveedor de datos** propiedad dinámica a "MSDASQL" especificando:

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 También puede establecer o recuperar una propiedad dinámica especificando su nombre como índice de la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) propiedad. Por ejemplo, en el ejemplo de código siguiente se obtiene y se imprime el valor actual de la **proveedor de datos** propiedad dinámica, a continuación, establece un valor nuevo si cn. DataProvider se ha establecido en "MSDataShape" (directa o indirectamente a través de la cadena de conexión) y no se ha abierto la conexión:

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  La propiedad dinámica, **proveedor de datos**, se puede establecer solo en una no abierto **conexión** objeto. Una vez que se abre la conexión, el **proveedor de datos** propiedad pasa a ser de solo lectura.

 Para obtener más información sobre la forma de datos, vea [dar forma a datos](../../../ado/guide/data/data-shaping-overview.md).

## <a name="see-also"></a>Vea también
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
