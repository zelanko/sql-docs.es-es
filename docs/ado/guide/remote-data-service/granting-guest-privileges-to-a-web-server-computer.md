---
title: Conceder privilegios de invitado a un equipo servidor Web | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21c4eae0608e433ed3ca7888091a7c658726192d
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557832"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Concesión de privilegios de invitado a un equipo del servidor web
La cuenta anónima de servidor Web (IUSR_*ComputerName*) debe agregarse a los invitados grupo local en el equipo servidor Web para utilizar RDS.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Para conceder privilegios de invitado a un equipo servidor Web  
  
1.  En el equipo de Microsoft Windows 2000 Server, haga clic en **iniciar**, apunte a **programas**, apunte a **herramientas administrativas**y, a continuación, haga clic en **equipo Administración**.  
  
2.  En el árbol de consola, en **usuarios y grupos locales**, haga clic en **grupos**.  
  
3.  Seleccione el **invitados** grupo local. Desde el **acción** menú, elija **propiedades**.  
  
4.  En el **invitados propiedades** cuadro de diálogo, haga clic en **agregar**.  
  
5.  Si la cuenta anónima de servidor Web no aparece en la lista en el **Seleccionar usuarios o grupos** diálogo cuadro, escriba su nombre (IUSR_*ComputerName*) en el cuadro vacío inferior y, a continuación, haga clic en **agregar** .  
  
6.  Haga clic en **Aceptar**.


