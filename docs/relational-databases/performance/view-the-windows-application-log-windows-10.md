---
title: Ver el registro de aplicaciones de Windows (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2e6e721948c2e875a5f9d6e100cdb29f928b4042
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85655264"
---
# <a name="view-the-windows-application-log-windows-10"></a>Ver el registro de aplicaciones de Windows (Windows 10)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para usar el registro de aplicaciones de Windows, todas las sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escriben los eventos nuevos en ese registro. A diferencia del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se crea un nuevo registro de aplicación cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="view-the-windows-application-log"></a>Ver el registro de aplicaciones de Windows  
  
1. En la **barra de búsqueda**, escriba **Visor de eventos** y, después, seleccione la aplicación de escritorio **Visor de eventos**.
  
2. En **Visor de eventos**, abra **Registros de aplicaciones y servicios**.

3. Los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se identifican con la entrada **MSSQLSERVER**(las instancias con nombre se identifican con **MSSQL$** _<nombre_de_instancia>_ ) en la columna **Origen**. Los eventos del Agente SQL Server se identifican con la entrada SQLSERVERAGENT (para las instancias con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se identifican con **SQLAgent$** \<*instance_name*>). Los eventos del servicio Microsoft Search se identifican con la entrada **Microsoft Search**.  
  
4. Para ver el registro de un equipo diferente, haga clic con el botón derecho en **Visor de eventos (local)** . Seleccione **Conectarse a otro equipo** y rellene los campos para completar el cuadro de diálogo **Seleccionar equipo**.  
  
5. Si quiere, para mostrar solamente eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el menú **Ver**, seleccione **Filtro**. En la lista **Origen del evento**, seleccione **MSSQLSERVER**. Para ver solo los eventos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **SQLSERVERAGENT** en la lista **Origen del evento** .  
  
6. Para ver más información acerca de un evento, haga doble clic en el suceso.  
  
## <a name="see-also"></a>Consulte también  
 [Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
