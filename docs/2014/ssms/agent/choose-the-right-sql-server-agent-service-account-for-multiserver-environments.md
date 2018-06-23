---
title: Elija la cuenta de servicio de agente de derecho de SQL Server para entornos multiservidor | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a4a25252eca826da83a856e8fcdde2ca6808a6de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203560"
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>Elegir la cuenta correcta del servicio del Agente SQL Server para entornos multiservidor
  La cuenta de Windows que elija para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede afectar al comportamiento de un entorno multiservidor, como se indica a continuación:  
  
-   Si ejecuta el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una cuenta que no sea miembro del grupo de administradores de Windows local, el alta de los servidores de destino en los servidores maestros puede generar un error. Si lo hace, se devuelve un mensaje de error que indica lo siguiente:  
  
     Error en la operación de alta.  
  
     Reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solucionar este problema.  
  
-   Cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en la cuenta del sistema local, las operaciones entre el servidor maestro y el servidor de destino solo se admiten si ambos servidores residen en el mismo equipo. Si usa esta configuración, verá el siguiente mensaje cuando dé de alta los servidores de destino en un servidor maestro:  
  
     "Comprobar que la cuenta de inicio del agente de *<nombre_equipo_servidor_destino>* posea derechos para iniciar la sesión como servidor de destino".  
  
     Puede omitir este mensaje informativo. La operación de alta debe finalizar correctamente.  
  
 Para más información sobre cómo elegir una cuenta para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md).  
  
  