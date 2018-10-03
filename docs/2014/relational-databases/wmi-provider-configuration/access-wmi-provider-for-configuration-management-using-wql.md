---
title: Obtener acceso el proveedor WMI para la administración de configuración mediante WQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0b19bf27cdc94e70908f81523a092ba022c41601
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157685"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Obtener acceso al proveedor WMI para la administración de configuración mediante WQL
  En esta sección se describe cómo ejecutar instrucciones WQL (Lenguaje de consulta de Instrumental de administración de Windows) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con el proveedor WMI para la Administración de equipos.  
  
 En el ejemplo se usa un editor WQL, WBEMtest.exe, para ejecutar las consultas WQL con el proveedor WMI y enumerar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], protocolos de red y alias.  
  
### <a name="querying-services-using-wbemtest"></a>Consultar los servicios mediante WBEMtest  
  
1.  Desde el **iniciar** menú, haga clic en **ejecutar**y, a continuación, escriba `WBEMtest`.  
  
2.  El diálogo de WBEMtest.exe aparece. Haga clic en **Conectar**.  
  
3.  En el primer campo de texto, escriba el espacio de nombres del proveedor WMI de Administración de equipos: raíz\Microsoft\SqlServer\ComputerManagement11. Haga clic en **Conectar**.  
  
4.  Haga clic en **consulta**. Escriba una consulta que devuelve los servicios actuales que se ejecutan en el equipo local: **seleccione \* de SqlService.** Haga clic en **Aplicar**.  
  
5.  Además, refine la consulta agregando `WHERE ServiceName = "MSSQLSERVER"`.  
  
  
