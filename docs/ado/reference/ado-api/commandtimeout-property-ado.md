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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5bb74384e043130ccfe4c3399b363b25d40737c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632163"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout (propiedad, ADO)
Indica cuánto tiempo debe para esperar mientras se ejecuta un comando antes de terminar el intento y generar un error.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica, en segundos, cuánto tiempo debe para esperar que ejecute un comando. Valor predeterminado es 30.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CommandTimeout** propiedad en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto para permitir la cancelación de un [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) (método) llamar a, debido a los retrasos de red tráfico o con mucha actividad de uso del servidor. Si el intervalo se establece el **CommandTimeout** propiedad transcurre antes de que el comando completa la ejecución, se produce un error y ADO cancela el comando. Si establece la propiedad en cero, ADO esperará indefinidamente hasta que la ejecución está completa. Asegúrese de que el proveedor y origen de datos a la que está escribiendo código admiten la **CommandTimeout** funcionalidad.  
  
 El **CommandTimeout** en un **conexión** objeto no tiene ningún efecto el **CommandTimeout** en un **comando** objeto en el mismo **conexión**; es decir, el **comando** del objeto **CommandTimeout** propiedad no hereda el valor de la **conexión** del objeto **CommandTimeout** valor.  
  
 En un **conexión** objeto, el **CommandTimeout** propiedad sigue siendo lectura/escritura después de la **conexión** se abre.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propiedad ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
