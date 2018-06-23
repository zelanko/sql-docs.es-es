---
title: Obtener acceso a proveedor WMI de administración de configuración mediante WQL | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c3c9ced24edc7e7f3537a73d074cf7cd73128dc8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107159"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Obtener acceso al proveedor WMI para la administración de configuración mediante WQL
  En esta sección se describe cómo ejecutar instrucciones WQL (Lenguaje de consulta de Instrumental de administración de Windows) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con el proveedor WMI para la Administración de equipos.  
  
 En el ejemplo se usa un editor WQL, WBEMtest.exe, para ejecutar las consultas WQL con el proveedor WMI y enumerar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], protocolos de red y alias.  
  
### <a name="querying-services-using-wbemtest"></a>Consultar los servicios mediante WBEMtest  
  
1.  Desde el **iniciar** menú, haga clic en **ejecutar**y, a continuación, escriba `WBEMtest`.  
  
2.  El diálogo de WBEMtest.exe aparece. Haga clic en **Conectar**.  
  
3.  En el primer campo de texto, escriba el espacio de nombres del proveedor WMI de Administración de equipos: raíz\Microsoft\SqlServer\ComputerManagement11. Haga clic en **Conectar**.  
  
4.  Haga clic en **consulta**. Escriba una consulta que devuelva los servicios actuales que se ejecutan en el equipo local: **seleccione \* de SqlService.** Haga clic en **Aplicar**.  
  
5.  Además, refine la consulta agregando `WHERE ServiceName = "MSSQLSERVER"`.  
  
  