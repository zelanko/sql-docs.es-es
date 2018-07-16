---
title: Dar de alta un servidor de destino en un servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3005fedecb002b50c239f53f1726bb7b6c78e1bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315185"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Dar de alta un servidor de destino en un servidor maestro
  En este tema se describe el modo de agregar servidores de destino a una configuración de la administración multiservidor. Ejecute este procedimiento en el servidor maestro. en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server (SMO).  
  
 Para información sobre cómo la cuenta de Windows usada para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afecta a un entorno multiservidor, consulte [Crear un entorno multiservidor](create-a-multiserver-environment.md).  
  
 El cifrado SSL (Capa de sockets seguros) y la validación de certificados completos se habilita para las conexiones entre los servidores maestros y los servidores de destino de forma predeterminada. Para más información, [Establecer opciones de cifrado en servidores de destino](set-encryption-options-on-target-servers.md).  
  
 **En este tema**  
  
-   **Para dar de alta un servidor de destino, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, en **Agregar servidores de destino**.  
  
3.  Complete el Asistente para establecer servidor de destino, que le guía a través del proceso.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  Use el procedimiento almacenado `sp_msx_enlist`.  Para obtener más información, consulte [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> Usar objetos de administración de SQL Server (SMO)  
  
## <a name="see-also"></a>Vea también  
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)  
  
  
