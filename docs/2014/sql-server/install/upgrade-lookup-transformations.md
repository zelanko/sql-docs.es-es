---
title: Actualizar las transformaciones de búsqueda | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 159779bc43edf7d30182e86aee545e6e9db8135a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032376"
---
# <a name="upgrade-lookup-transformations"></a>Actualizar las transformaciones de búsqueda
  Al actualizar de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tiene la opción de modificar los paquetes para aprovechar las nuevas características de la transformación Búsqueda. La transformación admite los tipos de almacenamiento en memoria caché y las opciones de salida de datos disponibles en [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]. Para obtener más información sobre adicional los resultados de datos y almacenamiento en caché, consulte el [transformación búsqueda](../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
 En [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], los tipos de almacenamiento en caché disponibles son almacenamiento en caché completo, almacenamiento parcial y ningún almacenamiento en caché. En [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], puede configurar una transformación de Búsqueda para utilizar uno de estos tipos de almacenamiento en caché. Para obtener más información acerca de cómo implementar almacenamiento parcial o ningún almacenamiento en caché, consulte [implementar una búsqueda en el modo de caché parcial o en No Cache](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md). Para obtener información acerca de cómo implementar el almacenamiento en caché completa, consulte [implementar una transformación Búsqueda en modo de caché completa mediante el Administrador de conexiones de caché](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) y [implementar una transformación Búsqueda en modo de caché completa mediante OLE Administrador de conexiones de base de datos](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md).  
  
 En [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], la transformación Búsqueda tenía una entrada, una salida y una salida de error. Las filas del contenido de entrada que tenían entradas coincidentes se controlaron en el resultado de salida. Las filas del contenido de entrada que no tenían entradas coincidentes se trataron como errores y se pudieron redirigir a la salida de error. En [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], la transformación Búsqueda tiene dos resultados: un resultado coincidente y otro no coincidente.  
  
 De forma predeterminada, al ejecutar una transformación Búsqueda creada en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] trata las filas sin entradas coincidentes como errores y permite redirigir las filas a una salida de error. Tiene la opción de configurar la transformación Búsqueda para tratar las filas como no errores y redirigir las filas al resultado no coincidente.  
  
 Para obtener más información, consulte [Editor de transformación búsqueda &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
## <a name="see-also"></a>Vea también  
 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
