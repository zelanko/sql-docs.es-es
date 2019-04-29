---
title: Conceder permisos al servicio Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0c2caa68-7834-4ea0-bd77-4f3a7c86d634
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6c1c2a07d0d5ff16b2d5cc9637c1b305c4c51851
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62893630"
---
# <a name="grant-permissions-to-integration-services-service"></a>Conceder permisos para el servicio Integration Services
  En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], cuando se instalaba [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] todos los usuarios del grupo Usuarios tenía acceso al servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de forma predeterminada. Cuando instala la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], los usuarios no tienen acceso al servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . El servicio es seguro de forma predeterminada. Una vez instalado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el administrador debe conceder acceso al servicio.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Para conceder acceso al servicio Integration Services  
  
1.  Ejecute Dcomcnfg.exe. Dcomcnfg.exe proporciona una interfaz de usuario para modificar algunos valores de configuración del Registro.  
  
2.  En el diálogo **Servicios de componentes**, expanda el nodo Servicios de componente > Equipos > Mi PC > Configuración DCOM.  
  
3.  Haga clic en **Microsoft SQL Server Integration Services 12.0**y, a continuación, haga clic en **propiedades**.  
  
4.  En la pestaña **Seguridad** , haga clic en **Editar** en la sección **Permisos de inicio y activación** .  
  
5.  Agregue usuarios y asigne los permisos adecuados y, a continuación, haga clic en Aceptar.  
  
6.  Repita los pasos 4 a 5 para los permisos de acceso.  
  
7.  Reinicie SQL Server Management Studio.  
  
8.  Reinicie el Servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
  
