---
description: Propiedad ActiveCommand (ADO)
title: Propiedad ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e8c969c8e611c8e2bff76dc045a28a9c6d6ab96
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759945"
---
# <a name="activecommand-property-ado"></a>Propiedad ActiveCommand (ADO)
Indica el objeto de [comando](./command-object-ado.md) que creó el objeto de [conjunto de registros](./recordset-object-ado.md) asociado.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **valor de tipo Variant** que contiene un objeto **Command** . El valor predeterminado es una referencia de objeto null.  
  
## <a name="remarks"></a>Comentarios  
 La propiedad **ActiveCommand** es de solo lectura.  
  
 Si un objeto de **comando** no se utilizó para crear el **conjunto de registros**actual, se devuelve una referencia de objeto **null** .  
  
 Utilice esta propiedad para buscar el objeto de **comando** asociado cuando solo se le proporciona el objeto de **conjunto de registros** resultante.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad ActiveCommand (VB)](./activecommand-property-example-vb.md)   
 [Ejemplo de la propiedad ActiveCommand (JScript)](./activecommand-property-example-jscript.md)   
 [Ejemplo de la propiedad ActiveCommand (VC + +)](./activecommand-property-example-vc.md)   
 [Objeto Command (ADO)](./command-object-ado.md)