---
title: access check cache (opciones de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a82aa2872f5a1e1658ab3d736c2651253bb7cc74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62812048"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache (opciones de configuración del servidor)
  Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tiene acceso a los objetos de base de datos, la comprobación del acceso se almacena en memoria caché en una estructura interna denominada **memoria caché de resultados de comprobación de acceso**. Las opciones **access check cache quota** y **access check cache bucket count** controlan el número de entradas y de cubos de hash que se usan para **access check result cache**. En circunstancias excepcionales, el rendimiento se puede mejorar cambiando estas opciones.  
  
 Los valores predeterminados de 0 indican que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está administrando estas opciones. Microsoft solo recomienda cambiar estas opciones cuando lo indiquen los servicios de soporte al cliente de Microsoft.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
