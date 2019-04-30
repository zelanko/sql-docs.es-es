---
title: Propiedad de proveedor (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::get_Provider
- Connection15::PutProvider
- Connection15::put_Provider
- Connection15::GetProvider
- Connection15::Provider
helpviewer_keywords:
- Provider property [ADO]
ms.assetid: 0ff70e72-0061-4ffc-90fb-e3ea23129bb2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22ee1b88ee6065a49c53ae7024c93e869099ca3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280335"
---
# <a name="provider-property-ado"></a>Propiedad de proveedor (ADO)
Indica el nombre del proveedor para un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que indica el nombre del proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Use la **proveedor** propiedad para establecer o devolver el nombre del proveedor para una conexión. Esta propiedad también puede establecerse mediante el contenido de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad o el *ConnectionString* argumento de la [abierto](../../../ado/reference/ado-api/open-method-ado-connection.md) método; sin embargo, si un proveedor en más de un solo lugar durante la llamada a la **abierto** método puede tener resultados impredecibles. Si se especifica ningún proveedor, la propiedad predeterminado MSDASQL ([proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)).  
  
 El **proveedor** propiedad es de lectura/escritura cuando la conexión está cerrada y de solo lectura cuando se abre. El valor no surtirá efecto hasta que abra el **conexión** objeto o acceso a la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de la **conexión** objeto. Si la configuración no es válida, se produce un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo Provider y DefaultDatabase propiedades (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Ejemplo Provider y DefaultDatabase propiedades (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
