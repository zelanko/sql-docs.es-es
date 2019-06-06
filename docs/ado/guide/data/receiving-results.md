---
title: Recibir los resultados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edd070cc6f10829b597534d024d767de2a0c7e12
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701719"
---
# <a name="receiving-results"></a>Recibir los resultados
En ADO mayoría de los comandos produce cierta información que se devuelve al llamador. Para devolver el conjunto de filas de comandos, se reciben los resultados en un **Recordset** objeto, que es probablemente el más usado de los objetos ADO.  
  
 Hay varias maneras de recibir datos en un **Recordset** objeto desde un origen de datos, incluidas las llamadas a lo siguiente:  
  
-   [Método Connection.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Command.Execute](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Método Recordset.Open](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Recibir datos en un **Recordset** objeto concluye el proceso de obtención de datos, con la participación de un **conexión** objeto y un **comando** objeto, implícitamente o de forma explícita. En un sistema de la aplicación cliente/servidor típicos, todo el proceso de obtención de datos requiere un recorrido de ida y a través de la red de cada rellenado **Recordset**.  
  
 Para recibir varios conjuntos de resultados significa necesitaría realizar varios viajes de ida a través de la red, uno para cada conjunto de datos encapsulada en un **Recordset** objeto. Redes lentas o está congestionadas, lo que reduce el número de ciclos de ida y puede ayudar a mejorar el rendimiento de la aplicación. Por lo tanto, algunos proveedores ofrecen soporte técnico para recibir varios **Recordset**s en un viaje de ida y. Esto se explica en el tema siguiente:  
  
-   [Recibir varios conjuntos de registros](../../../ado/guide/data/receiving-multiple-recordsets.md)
