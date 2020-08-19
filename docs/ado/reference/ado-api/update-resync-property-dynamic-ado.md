---
description: Propiedad dinámica Update Resync (ADO)
title: 'Propiedad de resincronización de actualización: dinámica (ADO) | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 43657b3dddcf53f9aa9df507c646b7f23088f0ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441637"
---
# <a name="update-resync-property-dynamic-ado"></a>Propiedad dinámica Update Resync (ADO)
Especifica si el método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) va seguido de una operación de método [Resync](../../../ado/reference/ado-api/resync-method.md) implícita y, en ese caso, el ámbito de esa operación.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno o varios de los valores de [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) .  
  
## <a name="remarks"></a>Observaciones  
 Los valores de ADCPROP_UPDATERESYNC_ENUM pueden combinarse, excepto adResyncAll, que ya representa la combinación del resto de los valores.  
  
 La constante **adResyncConflicts** almacena los valores de resincronización como valores subyacentes, pero no invalida los cambios pendientes.  
  
 **Update Resync** es una propiedad dinámica anexada a la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) del objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) cuando la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
