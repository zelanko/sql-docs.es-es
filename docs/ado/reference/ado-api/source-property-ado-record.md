---
title: Propiedad Source (registro de ADO) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930933"
---
# <a name="source-property-ado-record"></a>Propiedad Source (Record ADO)
Indica el origen de datos o el objeto representado por el [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Variant** que indica la entidad representada por el **registro**.  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **source** devuelve el argumento de *origen* del método [Open](../../../ado/reference/ado-api/open-method-ado-record.md) del objeto **Record** . Puede contener una cadena de dirección URL absoluta o relativa. Se puede usar una dirección URL absoluta sin establecer la propiedad [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) para abrir directamente el objeto de **registro** . En este caso, se crea un objeto de **conexión** implícita.  
  
 La propiedad **source** también puede contener una referencia a un conjunto de **registros**ya abierto, que abre un objeto **Record** que representa la fila actual del **conjunto de registros**.  
  
 La propiedad **source** también podría contener una referencia a un objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) que devuelve una sola fila de datos del proveedor.  
  
 Si también se establece la propiedad **ActiveConnection** , la propiedad **source** debe apuntar a algún objeto que exista dentro del ámbito de esa conexión. Por ejemplo, en los espacios de nombres estructurados por árbol, si la propiedad **source** contiene una dirección URL absoluta, debe apuntar a un nodo que exista dentro del ámbito del nodo identificado por la dirección URL en la cadena de conexión. Si la propiedad **source** contiene una dirección URL relativa, se valida en el contexto establecido por la propiedad **ActiveConnection** .  
  
 La propiedad de **origen** es de lectura y escritura mientras se cierra el objeto de **registro** y es de solo lectura mientras el objeto de **registro** está abierto.  
  
> [!NOTE]
>  Las direcciones URL que usan el esquema http invocarán automáticamente el [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [direcciones URL absolutas y relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Source (propiedad, error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
