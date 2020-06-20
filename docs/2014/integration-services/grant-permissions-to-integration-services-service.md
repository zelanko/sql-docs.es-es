---
title: Conceder permisos para Integration Services servicio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0c2caa68-7834-4ea0-bd77-4f3a7c86d634
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7a71b6b18960ee5b457be339e8a98ada505a6dec
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966255"
---
# <a name="grant-permissions-to-integration-services-service"></a>Conceder permisos para el servicio Integration Services
  En versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], cuando se instalaba [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] todos los usuarios del grupo Usuarios tenía acceso al servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de forma predeterminada. Cuando instala la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], los usuarios no tienen acceso al servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . El servicio es seguro de forma predeterminada. Una vez instalado [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el administrador debe conceder acceso al servicio.  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Para conceder acceso al servicio Integration Services  
  
1.  Ejecute Dcomcnfg.exe. Dcomcnfg.exe proporciona una interfaz de usuario para modificar algunos valores de configuración del Registro.  
  
2.  En el cuadro de diálogo **Servicios de componente**, expanda el nodo Servicios de componente > Equipos > Mi PC > Configuración DCOM.  
  
3.  Haga clic con el botón secundario en **Microsoft SQL Server Integration Services 12,0**y, a continuación, haga clic en **propiedades**.  
  
4.  En la pestaña **Seguridad** , haga clic en **Editar** en la sección **Permisos de inicio y activación** .  
  
5.  Agregue usuarios y asigne los permisos adecuados y, a continuación, haga clic en Aceptar.  
  
6.  Repita los pasos 4 a 5 para los permisos de acceso.  
  
7.  Reinicie SQL Server Management Studio.  
  
8.  Reinicie el Servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
  
