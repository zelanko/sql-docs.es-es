---
title: Actualización dinámica de propiedad Resync (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43b8864d03e3ec2e563984e203779e5905a15813
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762766"
---
# <a name="update-resync-property-dynamic-ado"></a>Propiedad dinámica Update Resync (ADO)
Especifica si el [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método va seguido de un modo implícito [Resync](../../../ado/reference/ado-api/resync-method.md) operación del método y si es así, el ámbito de esa operación.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno o varios de los [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) valores.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de ADCPROP_UPDATERESYNC_ENUM se pueden combinar, excepto adResyncAll, que ya representa la combinación del resto de los valores.  
  
 La constante **adResyncConflicts** almacena los valores de resincronización como valores subyacentes, pero no reemplaza los cambios pendientes.  
  
 **Actualizar la resincronización** se anexa una propiedad dinámica a la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
