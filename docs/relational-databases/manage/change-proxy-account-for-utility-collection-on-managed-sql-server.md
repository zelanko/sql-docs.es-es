---
title: Cambio de la cuenta de Proxy para la recopilación de la utilidad administrada SQL Server | Microsoft Docs
description: Obtenga información sobre cómo usar SQL Server Management Studio a fin de cambiar la cuenta de proxy para el Conjunto de recopilación de la utilidad en una instancia administrada de SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 052f0e6c1e60c5753f879e325c7cfa0603ba4303
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85776040"
---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>Cambio de la cuenta de Proxy para la recopilación de la utilidad administrada SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe cómo cambiar la cuenta de proxy para el conjunto de recopilación de utilidades en una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>Para cambiar la cuenta de proxy para el conjunto de recopilación de utilidades en una instancia administrada de SQL Server  
  
1.  Quite la instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   En **Explorador de la utilidad** de SSMS, haga clic en el nodo **Instancias administradas** .  
  
    -   En la vista de lista del **Explorador de la utilidad**, haga clic con el botón derecho en el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccione **Quitar instancia administrada...** . Para obtener más información, vea [Quitar una instancia de SQL Server de la Utilidad de SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
2.  Vuelva a inscribir la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

    -   En el **Explorador de la utilidad** de SSMS, haga clic con el botón derecho en el nodo **Instancias administradas** y seleccione **Agregar instancia administrada...** .  
  
    -   Siga las indicaciones para completar el asistente y especifique la nueva cuenta de proxy.  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas de la Utilidad de SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
