---
title: CommandTimeout (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b708b2b79c22240468811732d2ffae0955ea204
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242785"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout (propiedad, ADO)
Indica cuánto tiempo se debe esperar mientras se ejecuta un comando antes de terminar el intento y generar un error.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** que indica, en segundos, cuánto tiempo se debe esperar para que se ejecute un comando. El valor predeterminado es 30.  
  
## <a name="remarks"></a>Observaciones  
 Use la propiedad **CommandTimeout** en un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o un objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) para permitir la cancelación de una llamada al método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) debido a retrasos por el tráfico de red o un uso intensivo del servidor. Si el intervalo establecido en la propiedad **CommandTimeout** transcurre antes de que el comando complete la ejecución, se produce un error y ADO cancela el comando. Si establece la propiedad en cero, ADO esperará indefinidamente hasta que se complete la ejecución. Asegúrese de que el proveedor y el origen de datos en el que está escribiendo código admiten la funcionalidad **CommandTimeout** .  
  
 La configuración de **CommandTimeout** en un objeto de **conexión** no tiene ningún efecto en la configuración de **CommandTimeout** en un objeto de **comando** de la misma **conexión**. es decir, la propiedad **CommandTimeout** del objeto de **comando** no hereda el valor del valor **CommandTimeout** del objeto de **conexión** .  
  
 En un objeto de **conexión** , la propiedad **CommandTimeout** sigue siendo de lectura/escritura una vez abierta la **conexión** .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades ActiveConnection, CommandText, CommandTimeout, CommandType, size y Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Ejemplo de las propiedades ActiveConnection, CommandText, CommandTimeout, CommandType, size y Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Ejemplo de las propiedades ActiveConnection, CommandText, CommandTimeout, CommandType, size y Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propiedad ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
