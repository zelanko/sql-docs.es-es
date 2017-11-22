---
title: Source (propiedad) (registro de ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords: Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2e379bb3e2fce7899125c208251c8a04da1ea95
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="source-property-ado-record"></a>Propiedad Source (Record ADO)
Indica el origen de datos o el objeto representado por la [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** valor que indica la entidad representada por la **registro**.  
  
## <a name="remarks"></a>Comentarios  
 El **origen** propiedad devuelve el *origen* argumento de la **registro** objeto [abiertos](../../../ado/reference/ado-api/open-method-ado-record.md) método. Puede contener una cadena de dirección URL absoluta o relativa. Se puede utilizar una dirección URL absoluta sin configuración de la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad que se va a abrir directamente el **registro** objeto. Un modo implícito **conexión** objeto se crea en este caso.  
  
 El **origen** propiedad también puede contener una referencia a una ya está abierto **Recordset**, que abre un **registro** objeto que representa la fila actual en el  **Conjunto de registros**.  
  
 El **origen** propiedad también podría incluir una referencia a un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que devuelve una sola fila de datos desde el proveedor.  
  
 Si el **ActiveConnection** también se establece la propiedad, el **origen** propiedad debe apuntar a un objeto que existe dentro del ámbito de esa conexión. Por ejemplo, en los espacios de nombres con estructura de árbol, si la **origen** propiedad contiene una dirección URL absoluta, debe apuntar a un nodo que exista en el ámbito del nodo identificado por la dirección URL en la cadena de conexión. Si el **origen** propiedad contiene una dirección URL relativa, a continuación, se valida en el contexto establecido la **ActiveConnection** propiedad.  
  
 El **origen** propiedad es de lectura/escritura a la **registro** objeto está cerrado y es de sólo lectura mientras el **registro** objeto está abierto.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Source (Error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
