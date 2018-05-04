---
title: Recibir resultados | Documentos de Microsoft
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
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3330d2989f5662693ff7aca720d2bf6e07e16e33
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="receiving-results"></a>Recibir los resultados
En ADO casi todos los comandos producir cierta información que se devuelve al llamador. Para devolver el conjunto de filas de comandos, se reciben los resultados en un **Recordset** objeto, que es probablemente el más usado de los objetos de ADO.  
  
 Hay varias maneras para recibir datos en un **Recordset** objeto desde un origen de datos, incluidas las llamadas a lo siguiente:  
  
-   [Método Connection.Execute (método)](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Command.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open (método)](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Recibir datos en un **Recordset** objeto concluye el proceso de obtención de datos, con la participación de un **conexión** objeto y un **comando** objeto, implícitamente o de forma explícita. En un sistema de aplicación cliente-servidor típico, todo el proceso de obtención de datos requiere un viaje de ida a través de la red de cada rellenado **conjunto de registros**.  
  
 Para recibir más de uno de los conjuntos de resultados significa que se necesita para realizar varios de ida y vuelta por la red, uno para cada conjunto de datos encapsulada en un **Recordset** objeto. Redes lentas o está congestionadas, lo que reduce el número de viajes de ida y puede ayudar a mejorar el rendimiento de la aplicación. Por lo tanto, algunos proveedores ofrecen soporte técnico para recibir varios **Recordset**s en un viaje de ida y. Esto se explica en el tema siguiente:  
  
-   [Recibir varios conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
