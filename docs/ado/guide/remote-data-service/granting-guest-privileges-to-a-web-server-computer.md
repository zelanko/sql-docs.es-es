---
title: Conceder privilegios de invitado a un equipo servidor Web | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3935d66bdd1dfb412f5410b245231036ae025823
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Conceder privilegios de invitado a un equipo servidor Web
La cuenta anónima de servidor Web (IUSR_*ComputerName*) debe agregarse al grupo local de invitados en el equipo servidor Web para utilizar RDS.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Para conceder privilegios de invitado a un equipo servidor Web  
  
1.  En el equipo de Microsoft Windows 2000 Server, haga clic en **iniciar**, seleccione **programas**, seleccione **herramientas administrativas**y, a continuación, haga clic en **equipo Administración**.  
  
2.  En el árbol de consola, en **usuarios y grupos locales**, haga clic en **grupos**.  
  
3.  Seleccione el **invitados** grupo local. Desde el **acción** menú, elija **propiedades**.  
  
4.  En el **propiedades de invitados** cuadro de diálogo, haga clic en **agregar**.  
  
5.  Si la cuenta anónima de servidor Web no aparece en la lista en la **Seleccionar usuarios o grupos** diálogo cuadro, escriba su nombre (IUSR_*ComputerName*) en el cuadro vacío inferior y, a continuación, haga clic en **agregar** .  
  
6.  Haga clic en **Aceptar**.


