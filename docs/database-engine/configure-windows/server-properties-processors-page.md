---
title: "Propiedades del servidor (página Procesadores) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b7667d7be2910280587e548eb2548e3224221d6
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="server-properties---processors-page"></a>Propiedades del servidor - Página Procesadores
  Utilice esta página para ver o modificar las opciones del procesador. Los valores de configuración de la afinidad del procesador solo se habilitan si hay más de un procesador instalado.  
  
## <a name="options"></a>Opciones  
 **Afinidad del procesador**  
 Asigna procesadores a subprocesos específicos para eliminar las recargas de procesador y reducir la migración de subprocesos entre los procesadores. Para obtener más información, vea [affinity mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md).  
  
 **Afinidad de E/S**  
 Enlaza las E/S de disco de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un subconjunto determinado de CPU. Para obtener más información, vea [affinity I/O mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md).  
  
 **Establecer automáticamente máscara de afinidad de procesador para todos los procesadores**  
 Permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definir la afinidad de los procesadores.  
  
 **Establecer automáticamente máscara de afinidad de E/S para todos los procesadores**  
 Permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definir la afinidad de E/S.  
  
 **Número máximo de subprocesos de trabajo**  
 0 permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecer de forma dinámica el número de subprocesos de trabajo. Este valor es el más adecuado para la mayor parte de los sistemas. No obstante, según la configuración del sistema, definir esta opción en un valor específico puede mejorar, a veces, el rendimiento. Para más información, consulte [Configure the max worker threads Server Configuration Option](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).  
  
 **Aumentar la prioridad de SQL Server**  
 Especifica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutarse con una prioridad de programación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows mayor que la de los demás procesos del mismo equipo. Para más información, consulte [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).  
  
 **Usar fibras de Windows (agrupación ligera)**  
 Utiliza fibras de Windows en lugar de subprocesos para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción no está disponible en Windows 2003 Server Edition. Para obtener más información, consulte [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
 **Valores configurados**  
 Muestra los valores configurados para las opciones de este panel. Si cambia estos valores, haga clic en **Valores actuales** para comprobar si los cambios han surtido efecto. Si no tienen, deberá reiniciarse primero la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valores actuales**  
 Presenta los valores actuales de las opciones de este panel. Estos valores son de solo lectura.  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
