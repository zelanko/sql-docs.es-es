---
title: Propiedades de TCP/IP (pestaña protocolos) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f7731e5ee583c4b1356c9a538ee41a3a475c613
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="tcpip-properties-protocols-tab"></a>Propiedades de TCP/IP (pestaña Protocolos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use el cuadro de diálogo **Propiedades de TCP/IP** para configurar las opciones para el protocolo TCP/IP. Haga clic en **TCP/IP** en el panel izquierdo para mostrar configuraciones de direcciones IP individuales en el panel de detalles.  
  
 Es necesario reiniciar Microsoft SQL Server para que se apliquen los cambios.  
  
## <a name="options"></a>Opciones  
 **Enabled**  
 Los valores posibles son **Yes** y **No**.  
  
 **Keep Alive**  
 Especifique el intervalo (en milisegundos) en el que los paquetes de mantenimiento de conexión se transmitirán para comprobar si el equipo que está en la parte remota de una conexión todavía está disponible.  
  
 **Listen All**  
 Especifique si SQL Server escuchará en todas las direcciones IP que están enlazadas a tarjetas de red en el equipo. Si se establece en **No**, configure cada dirección IP por separado con el cuadro de diálogo de propiedades de cada dirección IP. Si se establece en **Yes**, la configuración del cuadro de propiedades de **IPAll** se aplicará en todas las direcciones IP. El valor predeterminado es **Yes**.  
  
 **No Delay**  
 SQL Server no implementa cambios en esta propiedad.  
  
## <a name="see-also"></a>Ver también  
 [Elegir un protocolo de red](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Crear una cadena de conexión válida con TCP/IP](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
