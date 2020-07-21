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
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158763"
---
# <a name="access-check-cache-server-configuration-options"></a>access check cache (opciones de configuración del servidor)
Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tiene acceso a los objetos de base de datos, la comprobación del acceso se almacena en memoria caché en una estructura interna denominada **memoria caché de resultados de comprobación de acceso**. 
  
La opción de **número de cubos de caché de comprobación de acceso** controla el número de depósitos de hash que se usan para la caché de resultados de comprobación de acceso. 

La opción **Access check cache quota** controla el número de entradas que se almacenan en la caché de resultados de comprobación de acceso. Cuando se alcanza el número máximo de entradas, se quitan las entradas más antiguas de la caché de resultados de comprobación de acceso.
  
Los valores predeterminados de 0 indican que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está administrando estas opciones. De [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] a través de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , los valores predeterminados se traducen a las siguientes configuraciones internas:
-   En el caso de Access check cache bucket Count, el valor 0 establece un valor predeterminado de 256 cubos para la arquitectura x86 y 2.048 depósitos para arquitecturas x64 e IA-64.
-   Para la comprobación de acceso de la cuota de caché, el valor 0 establece un valor predeterminado de 1.024 entradas para la arquitectura x86 y de 28.192.048 depósitos para las arquitecturas x64 e IA-64.

En circunstancias excepcionales, el rendimiento se puede mejorar cambiando estas opciones. Por ejemplo, puede que desee reducir el tamaño de la caché de resultados de la comprobación de acceso si se usa demasiada memoria. O bien, puede que desee aumentar el tamaño de la caché de resultados de comprobación de acceso si experimenta un uso intensivo de la CPU cuando se vuelven a calcular los permisos.

> [!IMPORTANT]
> Microsoft solo recomienda cambiar estas opciones cuando lo indiquen los servicios de soporte al cliente de Microsoft.
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
