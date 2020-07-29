---
title: Designación de un servidor de reenvío de eventos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d05b8e386a3df5314433dbf505e3c7682740434c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749057"
---
# <a name="designate-an-events-forwarding-server"></a>Designación de un servidor de reenvío de eventos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo designar un servidor al que [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reenvía eventos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Observe que el reenvío de eventos se aplica a los eventos reenviados entre servidores, no a los eventos reenviados entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedadas en un único equipo. Tenga en cuenta también que para recibir eventos reenviados, el servidor de administración de alertas debe ser una instancia predeterminada de SQL Server.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>Para designar un servidor de reenvío de eventos  
  
1.  En el **Explorador de objetos** , haga clic en el signo más para expandir el servidor desde el que desea reenviar eventos a otro servidor.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server -** _nombre_de_servidor_, en **Seleccionar una página**, haga clic en **Avanzadas**.  
  
4.  En **Reenvío de eventos de SQL Server**, active la casilla **Reenviar eventos a otro servidor** .  
  
5.  En la lista **Servidor** , seleccione un servidor y, a continuación, en **Eventos**, realice una de las selecciones siguientes:  
  
    -   Seleccione la opción **No controlados** para reenviar solo los eventos que no han sido controlados por alertas locales.  
  
    -   Seleccione la opción **Todos los eventos** para reenviar todos los eventos, independientemente de si han sido controlados o no por alertas locales.  
  
6.  En la lista **Si el evento tiene una gravedad de o por encima de** , haga clic en el nivel de gravedad a partir del cual se reenvían los eventos al servidor seleccionado.  
  
7.  Cuando termine, haga clic en **Aceptar**.  
  
