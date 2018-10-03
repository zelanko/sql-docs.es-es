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
manager: craigg
ms.openlocfilehash: 648fd220988a0b32837ddcdf2b4c1c23de5e9f69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657113"
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
