---
title: Usar WQL para tener acceso al proveedor WMI
description: Use este ejemplo para ver cómo ejecutar Instrumental de administración de Windows instrucciones de lenguaje de consulta para el proveedor WMI para la administración de equipos en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7efe4f3f8456dc68171b804d7afd28f565a4fbe2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888247"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Obtener acceso al proveedor WMI para la administración de configuración mediante WQL
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En esta sección se describe cómo ejecutar instrucciones WQL (Lenguaje de consulta de Instrumental de administración de Windows) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con el proveedor WMI para la Administración de equipos.  
  
 En el ejemplo se usa un editor WQL, WBEMtest.exe, para ejecutar las consultas WQL con el proveedor WMI y enumerar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], protocolos de red y alias.  
  
### <a name="querying-services-using-wbemtest"></a>Consultar los servicios mediante WBEMtest  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**y, a continuación, escriba **WBEMTest**.  
  
2.  El diálogo de WBEMtest.exe aparece. Haga clic en **Conectar**.  
  
3.  En el primer campo de texto, escriba el espacio de nombres del proveedor WMI de Administración de equipos: raíz\Microsoft\SqlServer\ComputerManagement11. Haga clic en **Conectar**.  
  
4.  Haga clic en **Consulta**. Escriba una consulta que devuelva los servicios actuales que se ejecutan en el equipo local: **SELECT \* from SqlService.** Haga clic en **Aplicar**.  
  
5.  Refine la consulta agregando **Where ServiceName = "MSSQLSERVER"**.  
  
  
