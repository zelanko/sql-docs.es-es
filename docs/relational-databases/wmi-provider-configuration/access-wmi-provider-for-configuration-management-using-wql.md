---
title: Obtener acceso a proveedor WMI de administración de configuración mediante WQL | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cece73ebb5402fe2f725fedbcdf7cdc833d08265
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013182"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Obtener acceso al proveedor WMI para la administración de configuración mediante WQL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  En esta sección se describe cómo ejecutar instrucciones WQL (Lenguaje de consulta de Instrumental de administración de Windows) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con el proveedor WMI para la Administración de equipos.  
  
 En el ejemplo se usa un editor WQL, WBEMtest.exe, para ejecutar las consultas WQL con el proveedor WMI y enumerar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], protocolos de red y alias.  
  
### <a name="querying-services-using-wbemtest"></a>Consultar los servicios mediante WBEMtest  
  
1.  Desde el **iniciar** menú, haga clic en **ejecutar**y, a continuación, escriba **WBEMtest**.  
  
2.  El diálogo de WBEMtest.exe aparece. Haga clic en **Conectar**.  
  
3.  En el primer campo de texto, escriba el espacio de nombres del proveedor WMI de Administración de equipos: raíz\Microsoft\SqlServer\ComputerManagement11. Haga clic en **Conectar**.  
  
4.  Haga clic en **consulta**. Escriba una consulta que devuelva los servicios actuales que se ejecutan en el equipo local: **seleccione \* de SqlService.** Haga clic en **Aplicar**.  
  
5.  Refinar la consulta agregando **donde ServiceName = "MSSQLSERVER"**.  
  
  
