---
title: Registrar un objeto de negocios personalizada | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9db18a572fc82b05e75fb7bb286afb572fe500fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704240"
---
# <a name="registering-a-custom-business-object"></a>Registro de un objeto de negocios personalizado
Para iniciar correctamente un objeto de negocios personalizados (.dll o .exe) a través del servidor Web, ProgID del objeto comercial debe especificarse en el registro como se explica en este procedimiento. Esta característica RDS protege la seguridad del servidor Web al ejecutar sólo ejecutables autorizados.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Para MDAC 2.0 y versiones posterior y Windows DAC, el objeto de negocios de forma predeterminada, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), no se registra de forma predeterminada durante la instalación de Windows o MDAC DAC. Sin embargo, si **RDSServer.DataFactory** se registró como seguros para la ejecución en el equipo antes de la instalación, la entrada del registro se mantiene para la nueva instalación.  
  
### <a name="to-register-a-custom-business-object"></a>Para registrar un objeto de negocios personalizada:  
  
1.  Haga clic en **iniciar** y, a continuación, haga clic en **ejecutar**.  
  
2.  Tipo **RegEdit** y haga clic en **Aceptar**.  
  
3.  En el Editor del registro, navegue hasta la **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** clave del registro.  
  
4.  Seleccione el **ADCLaunch** clave y, a continuación, desde el **editar**menú, elija **New** y haga clic en **clave**.  
  
5.  Escriba el ProgID de su objeto de negocios personalizada y haga clic en **ENTRAR**. Deje el **valor** entrada en blanco.


