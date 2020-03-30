---
title: Propiedades del servidor (página Memoria) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.memory.f1
ms.assetid: 46a77d4e-ab92-49d3-a14b-423462e50715
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6eb32d81ccab79efa044ed4a21798bebe6ee3fd1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025473"
---
# <a name="server-properties---memory-page"></a>Propiedades del servidor (página Memoria)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice esta página para ver o modificar las opciones de memoria del servidor. Cuando **Cantidad mínima de memoria del servidor** está establecida en 0 y **Cantidad máxima de memoria del servidor** está establecida en 2147483647 MB, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede aprovechar la cantidad óptima de memoria en un momento dado, dependiendo de la cantidad de memoria que utilicen en ese momento el sistema operativo y otras aplicaciones. Al cambiar la carga del equipo y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , también cambia la memoria asignada. Puede limitar aún más esta asignación de memoria dinámica a los valores máximos y mínimos que se especifican a continuación.  
  
## <a name="options"></a>Opciones  
 **Cantidad mínima de memoria del servidor (en MB)**  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe empezar, al menos, con la cantidad mínima de memoria asignada y no debe liberar memoria por debajo de este valor. Establezca este valor basándose en el tamaño y la actividad de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Establezca siempre la opción en un valor razonable para asegurarse de que el sistema operativo no requiere demasiada memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no impide el rendimiento de Windows.  
  
 **Cantidad máxima de memoria del servidor (en MB)**  
 Especifica la cantidad máxima de memoria que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede asignar cuando se inicia y mientras se ejecuta. Puede establecer esta opción de configuración como un valor específico si sabe que se ejecutan varias aplicaciones al mismo tiempo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y desea que estas aplicaciones tengan memoria suficiente para ejecutarse. Si estas otras aplicaciones, por ejemplo, los servidores web o de correo electrónico, solo solicitan memoria cuando la necesitan, no establezca la opción, ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suministrará memoria cuando sea necesario. Sin embargo, a menudo las aplicaciones utilizan la memoria disponible cuando se inician y no solicitan más aunque sea necesario. Si una aplicación con este comportamiento se ejecuta en el mismo equipo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]simultáneamente, establezca la opción con un valor que garantice que la memoria que requiere la aplicación no está asignada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cantidad de memoria mínima que puede especificar para **max server memory** es 128 MB. (64 megabytes (MB) para sistemas de 32 bits anteriores).  
  
 **Memoria de creación de índice (en KB, 0 = memoria dinámica)**  
 Especifica la cantidad de memoria (en KB) que se va a utilizar durante la ordenación en la creación de índices. El valor predeterminado de cero permite la asignación dinámica y funcionará en la mayoría de los casos sin ajustes adicionales; sin embargo, el usuario puede escribir un valor diferente, entre 704 y 2147483647.  
  
> [!NOTE]  
>  No se admiten los valores de 1 a 703. Si se escribe un valor en este intervalo, el campo reemplazará el valor especificado con 704.  
  
 **Cantidad mínima de memoria por consulta (en KB)**  
 Especifica la cantidad de memoria (en KB) que se va a asignar para la ejecución de una consulta. El usuario puede establecer el valor desde 512 hasta 2147483647 KB. El valor predeterminado es 1024 KB.  
  
 **Valores configurados**  
 Muestra los valores configurados para las opciones de este panel. Si cambia estos valores, haga clic en **Valores actuales** para comprobar si los cambios han surtido efecto. Si no tienen, deberá reiniciarse primero la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valores actuales**  
 Muestra los valores actuales de las opciones de este panel. Estos valores son de solo lectura.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
