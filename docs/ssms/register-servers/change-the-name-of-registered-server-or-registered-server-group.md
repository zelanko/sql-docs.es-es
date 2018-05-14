---
title: Cambiar el nombre de un servidor registrado o un grupo de servidores registrados | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-registration
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9a1455eadba4fe4d8ec2072df8f5f5fc11f29ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Cambiar el nombre de un servidor registrado o un grupo de servidores registrados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  En este tema se describe cómo cambiar el nombre de un servidor o un grupo de servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este nombre se puede cambiar en cualquier momento. El hecho de cambiar el nombre de un servidor en Servidores registrados solo cambia el nombre que se visualiza. Para conectarse a otro servidor, debe editar las propiedades de conexión del servidor registrado.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
En el menú, vaya a **Vista\\Servidores registrados** para abrir el panel **Servidores registrados**.  
#### <a name="to-change-the-name-of-a-server"></a>Para cambiar el nombre de un servidor  
  
1.  En **Servidores registrados**, expanda **Motor de base de datos** y, luego, **Grupos de servidores locales**.  

2.  Haga clic con el botón derecho en un servidor y seleccione **Propiedades** para abrir la ventana de diálogo **Editar propiedades de registro de servidor** .
  
3.  En el cuadro de texto **Nombre del servidor registrado** , escriba el nuevo nombre del registro del servidor y, luego, haga clic en **Guardar**.  
  
#### <a name="to-change-the-name-of-a-server-group"></a>Para cambiar el nombre de un grupo de servidores  
  
1.  En **Servidores registrados**, expanda **Motor de base de datos** y, luego, **Grupos de servidores locales**.  

2.  Haga clic con el botón derecho en un grupo de servidores y seleccione **Propiedades** para abrir la ventana de diálogo **Editar propiedades de registro de servidor** . 
  
3.  En el cuadro de texto **Nombre del grupo** , escriba el nuevo nombre del grupo de servidores y, luego, haga clic en **Guardar**.  
  
## <a name="see-also"></a>Ver también  
 [Cambiar el registro de un servidor &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  
