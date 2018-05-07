---
title: Propiedad ParentURL (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51a7a476352519f4756e4e8f19166aac3c84d7da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="parenturl-property-ado"></a>Propiedad ParentURL (ADO)
Indica una cadena de dirección URL absoluta que apunta al elemento primario [registro](../../../ado/reference/ado-api/record-object-ado.md) del elemento actual **registro** objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que indica la dirección URL del elemento primario **registro**.  
  
## <a name="remarks"></a>Comentarios  
 El **ParentURL** propiedad depende del origen utilizado para abrir el **registro** objeto. Por ejemplo, el **registro** se puede abrir con un origen que contiene un nombre de ruta de acceso relativa de un directorio al que hace referencia el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
 Imagine que "second" es una carpeta incluida en "first". Abra la **registro** objeto mediante la sintaxis siguiente:  
  
```  
record.ActiveConnection = "http://first"  
record.Open "second"  
```  
  
 Ahora, el valor de `the` **ParentURL** propiedad es `"http://first"`, el mismo como **ActiveConnection**.  
  
 El origen también puede ser una dirección URL absoluta, como `"http://first/second"`. El **ParentURL** propiedad es, a continuación, `"http://first"`, el nivel superior `"second"`.  
  
 Esta propiedad puede ser un valor nulo si:  
  
-   No hay ningún elemento primario para el objeto actual; Por ejemplo, si la **registro** objeto representa la raíz de un directorio.  
  
-   El **registro** objeto representa una entidad que no se puede especificar una dirección URL.  
  
 Esta propiedad es de solo lectura.  
  
> [!NOTE]
>  Esta propiedad sólo es compatible con proveedores de código fuente del documento, como el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [registros y campos proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
> [!NOTE]
>  Si el registro actual contiene un registro de datos de ADO **Recordset**, acceso a la **ParentURL** propiedad provoca un error de tiempo de ejecución, que indica que no es posible ninguna dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
