---
title: "Comprobación del subsistema de entrada y salida de disco para problemas de retraso de E/S | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: eaaf5e692a33c6f418d6a117b7f1231c20d2ba71
ms.lasthandoff: 04/11/2017

---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Check Disk Input and Output Subsystem for IO Delay Problems
  Esta regla comprueba si existe el mensaje de error 833 en el registro de eventos. Este mensaje indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha emitido una solicitud de lectura o escritura desde el disco y que la solicitud ha tardado más de 15 segundos en volver. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notifica este error, que indica un problema con el subsistema de E/S de disco. Estos largos retrasos pueden dañar gravemente el rendimiento del entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Solucione este error examinando el registro de eventos del sistema para localizar mensajes de error relacionados con el hardware. Examine también registros específicos de hardware si están disponibles.  
  
 Use el Monitor de rendimiento para examinar los siguientes contadores:  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 Por ejemplo, el tiempo de Average Disk Sec/Transfer en un equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele ser inferior a 15 milisegundos. Si el valor de Average Disk Sec/Transfer aumenta, esto indica que el subsistema de E/S de disco no está tratando la demanda de E/S de forma óptima.  
  
## <a name="for-more-information"></a>Para obtener más información  
   
  
 [Artículo 897284 de Microsoft Knowledge Base](http://go.microsoft.com/fwlink/?linkid=117743)  
  
 [Elementos fundamentales de E/S de SQL Server, capítulo 2](http://go.microsoft.com/fwlink/?LinkId=69370)  
  
  

