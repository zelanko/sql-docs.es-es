---
title: allow updates (opción de configuración del servidor) | Microsoft Docs
description: Obtenga información sobre la opción de configuración obsoleta de SQL Server "allow updates". Vea cómo el uso de esta opción provoca un error en las instrucciones RECONFIGURE.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6e4cde898f4b7c95fa3dd46d23d073ba47b5fb43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725257"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates (opción de configuración del servidor)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta opción aún está presente en el procedimiento almacenado **sp_configure** , pero su funcionalidad no está disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La opción no tiene ningún efecto. No se permiten las actualizaciones directas a las tablas del sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Si se cambia la opción **allow updates** , se producirá un error en la instrucción RECONFIGURE. Los cambios en la opción **allow updates** deben eliminarse de todos los scripts.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
