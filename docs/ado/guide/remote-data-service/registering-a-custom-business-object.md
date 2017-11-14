---
title: Registrar un objeto comercial personalizado | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be54505545b80211ec34216a67596c32ca8ce2b2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="registering-a-custom-business-object"></a>Registrar un objeto comercial personalizado
Para iniciar correctamente un objeto comercial personalizado (.dll o .exe) a través del servidor Web, se debe especificar ProgID del objeto de negocios en el registro como se explica en este procedimiento. Esta característica RDS protege la seguridad del servidor Web al ejecutar sólo ejecutables autorizados.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Para MDAC 2.0 y versiones posteriores y Windows DAC, el objeto de negocios de forma predeterminada, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), no se registra de forma predeterminada durante la instalación de MDAC/Windows DAC. Sin embargo, si **RDSServer.DataFactory** se registró como seguros para la ejecución en el equipo antes de la instalación, la entrada del registro se mantiene para la nueva instalación.  
  
### <a name="to-register-a-custom-business-object"></a>Para registrar un objeto comercial personalizado:  
  
1.  Haga clic en **iniciar** y, a continuación, haga clic en **ejecutar**.  
  
2.  Tipo de **RegEdit** y haga clic en **Aceptar**.  
  
3.  En el Editor del registro, desplácese hasta la **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** clave del registro.  
  
4.  Seleccione el **ADCLaunch** clave y, a continuación, desde el **editar**menú, elija **New** y haga clic en **clave**.  
  
5.  Escriba el ProgID de su objeto de negocios personalizada y haga clic en **ENTRAR**. Deje el **valor** entrada en blanco.



