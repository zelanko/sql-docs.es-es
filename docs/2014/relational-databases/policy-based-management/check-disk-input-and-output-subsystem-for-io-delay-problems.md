---
title: Comprobación del subsistema de entrada y salida de disco para problemas de retraso de E/S | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 59c6c98a9b401b220e912617e9c5693b5d782a2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110455"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Comprobación del subsistema de entrada y salida de disco para problemas de retraso de E/S
  Esta regla comprueba si existe el mensaje de error 833 en el registro de eventos. Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha emitido una solicitud de lectura o escritura desde el disco y que la solicitud ha tardado más de 15 segundos en volver. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notifica este error, que indica un problema con el subsistema de E/S de disco. Estos largos retrasos pueden dañar gravemente el rendimiento del entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Solucione este error examinando el registro de eventos del sistema para localizar mensajes de error relacionados con el hardware. Examine también registros específicos de hardware si están disponibles.  
  
 Use el Monitor de rendimiento para examinar los siguientes contadores:  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 Por ejemplo, el tiempo de Average Disk Sec/Transfer en un equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele ser inferior a 15 milisegundos. Si el valor de Average Disk Sec/Transfer aumenta, esto indica que el subsistema de E/S de disco no está tratando la demanda de E/S de forma óptima.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [MSSQLSERVER_833](../errors-events/mssqlserver-833-database-engine-error.md)  
  
 [Artículo 897284 de Microsoft Knowledge Base](http://go.microsoft.com/fwlink/?linkid=117743)  
  
 [Elementos fundamentales de E/S de SQL Server, capítulo 2](http://go.microsoft.com/fwlink/?LinkId=69370)  
  
  
