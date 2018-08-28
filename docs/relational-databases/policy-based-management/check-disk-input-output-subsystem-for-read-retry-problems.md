---
title: Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 30d264f29716d954e0b627e1b3ce14c34de86660
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40412669"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Comprobación de la existencia de problemas de reintento de lectura en el subsistema de entrada y salida del disco
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si existe el mensaje de error 825 de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el registro de eventos. Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo leer los datos del disco al primer intento. Este mensaje indica un problema importante con el subsistema de E/S de disco. Este mensaje no indica actualmente un problema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, el problema de disco podría producir la pérdida de datos o daños en la base de datos si no se resuelve.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Las siguientes acciones podrían ayudarle a detectar y resolver el problema de hardware subyacente:  
  
-   Revise el registro de errores y el texto variable de este mensaje para obtener pistas que expliquen el problema.  
  
-   Compruebe el sistema de disco. El problema podría estar relacionado con discos, controladores de discos, tarjetas de matriz o unidades de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las utilidades más recientes a fin de comprobar el estado del sistema de disco.  
  
-   Póngase en contacto con el fabricante del disco para obtener las últimas actualizaciones del controlador.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [Elementos fundamentales de E/S de SQL Server, capítulo 2](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
