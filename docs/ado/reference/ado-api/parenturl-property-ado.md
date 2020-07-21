---
title: Propiedad ParentURL (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: rothja
ms.author: jroth
ms.openlocfilehash: cb0669abc03da183fc70c289631fed67bb41829d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761993"
---
# <a name="parenturl-property-ado"></a>Propiedad ParentURL (ADO)
Indica una cadena de dirección URL absoluta que apunta al [registro](../../../ado/reference/ado-api/record-object-ado.md) primario del objeto de **registro** actual.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **cadena** que indica la dirección URL del **registro**primario.  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **ParentURL** depende del origen utilizado para abrir el objeto de **registro** . Por ejemplo, el **registro** se puede abrir con un origen que contiene un nombre de ruta de acceso relativa de un directorio al que hace referencia la propiedad [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) .  
  
 Supongamos que "Second" es una carpeta contenida en "First". Abra el objeto de **registro** con la siguiente sintaxis:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 Ahora, el valor de la `the` propiedad **ParentURL** es `"https://first"` , el mismo que el de **ActiveConnection**.  
  
 El origen también puede ser una dirección URL absoluta como, por ejemplo, `"https://first/second"` . La propiedad **ParentURL** es entonces `"https://first"` el nivel superior `"second"` .  
  
 Esta propiedad puede ser un valor NULL si:  
  
-   No hay ningún elemento primario para el objeto actual; por ejemplo, si el objeto **Record** representa la raíz de un directorio.  
  
-   El objeto **Record** representa una entidad que no se puede especificar con una dirección URL.  
  
 Esta propiedad es de solo lectura.  
  
> [!NOTE]
>  Esta propiedad solo es compatible con proveedores de origen de documentos, como el [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [registros y campos proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  Las direcciones URL que usan el esquema http invocarán automáticamente el [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [direcciones URL absolutas y relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Si el registro actual contiene un registro de datos de un **conjunto de registros**ADO, el acceso a la propiedad **ParentURL** produce un error en tiempo de ejecución, lo que indica que no es posible ninguna dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
