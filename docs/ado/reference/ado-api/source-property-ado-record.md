---
title: Source (Record ADO) de la propiedad | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1870d8cd8253e1b6de74ce093d51ca6e33c5c6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930933"
---
# <a name="source-property-ado-record"></a>Propiedad Source (Record ADO)
Indica el origen de datos o el objeto representado por la [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** valor que indica la entidad representada por el **registro**.  
  
## <a name="remarks"></a>Comentarios  
 El **origen** propiedad devuelve el *origen* argumento de la **registro** objeto [abierto](../../../ado/reference/ado-api/open-method-ado-record.md) método. Puede contener una cadena de dirección URL absoluta o relativa. Se puede usar una dirección URL absoluta sin establecer el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad pueden abrir directamente el **registro** objeto. Implicit **conexión** objeto se crea en este caso.  
  
 El **origen** propiedad también puede contener una referencia a una ya está abierta **Recordset**, que abre un **registro** objeto que representa la fila actual en el  **Conjunto de registros**.  
  
 El **origen** propiedad también podría incluir una referencia a un [comando](../../../ado/reference/ado-api/command-object-ado.md) object que devuelve una sola fila de datos del proveedor.  
  
 Si el **ActiveConnection** también se establece la propiedad, el **origen** propiedad debe señalar a un objeto que existe dentro del ámbito de esa conexión. Por ejemplo, en la estructura de árbol de espacios de nombres, si el **origen** propiedad contiene una dirección URL absoluta, debe señalar a un nodo que exista en el ámbito del nodo identificado por la dirección URL en la cadena de conexión. Si el **origen** propiedad contiene una dirección URL relativa, a continuación, se valida en el contexto establecido por la **ActiveConnection** propiedad.  
  
 El **origen** propiedad es de lectura/escritura, mientras el **registro** objeto está cerrado y es de solo lectura mientras la **registro** objeto está abierto.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Source (Error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
