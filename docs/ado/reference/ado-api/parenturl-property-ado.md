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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 65704cea2a396e0f03de4bbcdc9f031f4c9af583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703464"
---
# <a name="parenturl-property-ado"></a>Propiedad ParentURL (ADO)
Indica una cadena de dirección URL absoluta que apunta al elemento primario [registro](../../../ado/reference/ado-api/record-object-ado.md) del actual **registro** objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que indica la dirección URL del elemento primario **registro**.  
  
## <a name="remarks"></a>Comentarios  
 El **ParentURL** propiedad depende de la fuente utilizada para abrir el **registro** objeto. Por ejemplo, el **registro** puede abrirse con un origen que contiene un nombre de ruta de acceso relativa de un directorio al que hace referencia el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
 Supongamos que "second" es una carpeta incluida en "first". Abra el **registro** objeto mediante la sintaxis siguiente:  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 Ahora, el valor de `the` **ParentURL** propiedad es `"https://first"`, el mismo como **ActiveConnection**.  
  
 El origen también puede ser una dirección URL absoluta como `"https://first/second"`. El **ParentURL** propiedad es, a continuación, `"https://first"`, el nivel superior `"second"`.  
  
 Esta propiedad puede ser un valor nulo si:  
  
-   No hay ningún elemento primario del objeto actual; Por ejemplo, si la **registro** objeto representa la raíz de un directorio.  
  
-   El **registro** objeto representa una entidad que no se puede especificar con una dirección URL.  
  
 Esta propiedad es de solo lectura.  
  
> [!NOTE]
>  Esta propiedad solo es compatible con proveedores de código fuente del documento, como el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [registros y campos proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Si el registro actual contiene un registro de datos de ADO **Recordset**, al acceder a la **ParentURL** propiedad provoca un error de tiempo de ejecución, que indica que no es posible ninguna dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
