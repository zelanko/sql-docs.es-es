---
title: Propiedades de TCP/IP (pestaña protocolos) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 038c179061c2210278dbfadea236be9dc0bcb09f
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728292"
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
  
## <a name="see-also"></a>Consulte también  
 [Elegir un protocolo de red](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Crear una cadena de conexión válida con TCP/IP](creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
