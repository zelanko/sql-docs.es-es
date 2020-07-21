---
title: open objects (opción de configuración del servidor) | Microsoft Docs
description: Obtenga información sobre la opción de configuración deshabilitada "Abrir objetos". Vea cómo ahora SQL Server administra el número de objetos de base de datos abiertos.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- open objects option
ms.assetid: c8424d3c-86ba-4cc5-bf0c-be4ce44bdd04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0bbcb11a80f06eae10e5481c965e9216cc84695e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773618"
---
# <a name="open-objects-server-configuration-option"></a>open objects (opción de configuración del servidor)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta opción sigue presente en **sp_configure**, si bien su funcionalidad se ha deshabilitado en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La opción no tiene ningún efecto. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el número de objetos de bases de datos abiertos se administra dinámicamente y solo está limitado por la memoria disponible. La opción **open objects** está disponible en **sp_configure** por razones de compatibilidad con versiones anteriores de los scripts existentes.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
