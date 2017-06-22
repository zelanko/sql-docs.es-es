---
title: Dar de baja varios servidores de destino desde un servidor maestro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d24f986e0274592b8984c9bf5d493261781b8f77
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Dar de baja varios servidores de destino desde un servidor maestro
En este tema se describe cómo dar de baja varios servidores de destino desde una configuración de administración multiservidor en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Ejecute este procedimiento en el servidor maestro.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>Para dar de baja varios servidores de destino desde un servidor maestro  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración multiservidor**y, luego, haga clic en **Administrar servidores de destino**.  
  
3.  Haga clic en **Exponer instrucciones**, y, a continuación, en la lista **Tipo de instrucción** , haga clic en **Dar de baja**.  
  
4.  En **Destinatarios**, realice una de las siguientes acciones:  
  
    -   Haga clic en **Todos los servidores de destino** para dar de baja todos los servidores de destino de este servidor principal. Utilice esta opción si desea desinstalar totalmente la configuración de la administración multiservidor actual.  
  
    -   Haga clic en **Estos servidores de destino**y, a continuación, active la casilla **Seleccionar** correspondiente para dar de baja algunos servidores de destino, pero no todos, de este servidor principal.  
  
## <a name="see-also"></a>Vea también  
[Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)  
[Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Defect a Target Server from a Master Server](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  

