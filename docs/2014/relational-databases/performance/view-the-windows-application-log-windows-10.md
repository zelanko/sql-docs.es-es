---
title: Ver el registro de aplicación Windows (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72b47b9dada82f66ec0cb97b1f9a4dec8aebdbdf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748217"
---
# <a name="view-the-windows-application-log-windows"></a>Ver el registro de aplicación Windows (Windows)
  Si se configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para utilizar el registro de aplicación de Windows, todas las sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribirán los nuevos eventos en el registro. A diferencia del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se crea un nuevo registro de aplicación cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="to-view-the-windows-application-log"></a>Para ver el registro de aplicación Windows  
  
1.  En el menú **Inicio** , seleccione **Todos los programas**, **Herramientas administrativas**y, a continuación, haga clic en **Visor de eventos**.  
  
2.  En el Visor de eventos, haga clic en **Aplicación**.  
  
3.  Los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se identifican con la entrada **MSSQLSERVER**(las instancias con nombre se identifican con **MSSQL$***<nombre_de_instancia>*) en la columna **Origen**. Los eventos del Agente SQL Server se identifican con la entrada SQLSERVERAGENT (para las instancias con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se identifican con **SQLAgent$**\<*nombre_de_instancia*>). Los eventos del servicio Microsoft Search se identifican con la entrada **Microsoft Search**.  
  
4.  Para ver el registro de otro equipo, haga clic con el botón derecho en **Visor de eventos**, haga clic en **Conectar con otro equipo** y complete el cuadro de diálogo **Seleccionar equipo**.  
  
5.  Opcionalmente, para que solo se muestren los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el menú **Ver** , haga clic en **Filtro**y, en la lista **Origen del evento** , seleccione **MSSQLSERVER**. Para ver solo los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **SQLSERVERAGENT** en la lista **Origen del evento** .  
  
6.  Para ver más información acerca de un evento, haga doble clic en el suceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
  
