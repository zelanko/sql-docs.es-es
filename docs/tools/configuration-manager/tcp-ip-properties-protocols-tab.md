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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b8e961af919f3d92dad4aba5d87e910e341ce07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797415"
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
  
  
