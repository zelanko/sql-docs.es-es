---
title: allow updates (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6cf28b18bcad06be7383b98dee72810c4e6157c0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62786994"
---
# <a name="allow-updates-server-configuration-option"></a>allow updates (opción de configuración del servidor)
  Esta opción aún está presente en el procedimiento almacenado **sp_configure** , pero su funcionalidad no está disponible en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La opción no tiene ningún efecto. No se permiten las actualizaciones directas a las tablas del sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Si se cambia la opción **allow updates** , se producirá un error en la instrucción RECONFIGURE. Los cambios en la opción **allow updates** deben eliminarse de todos los scripts.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
