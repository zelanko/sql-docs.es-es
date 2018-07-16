---
title: Intercalación de servidor del motor de base de datos incompatible (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e182df78fc7faae8a50092fd51a8f2c0964fe2bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286651"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Intercalación del servidor de motor de base de datos incompatible (Asesor de actualizaciones)
  Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para utilizar una intercalación de servidor incompatible.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa una instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurado para utilizar una intercalación de servidor incompatible.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint usa la arquitectura de servicios compartidos de SharePoint. SharePoint no admite [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para las intercalaciones de servidor o que distinguen entre mayúsculas y minúsculas o las intercalaciones de servidor binarias. Entre las intercalaciones incompatibles se incluyen las que son binarias o distinguen entre mayúsculas y minúsculas de forma predeterminada, y las intercalaciones base que son compatibles de forma predeterminada, pero se han configurado con alguno de los designadores de intercalación siguientes:  
  
-   **Binario**  
  
-   **Distingue mayúsculas de minúsculas**  
  
-   **Binario-punto de código**  
  
 Debido a que la intercalación de servidor actual de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] es incompatible, la actualización se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 La propiedad de intercalación del servidor de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no se puede cambiar. No podrá completar una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Deberá migrar la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un servidor nuevo que use una intercalación del servidor compatible. Para obtener más información, vea:  
  
-   [Actualizar y migrar Reporting Services](http://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Seleccionar una intercalación de SQL Server](http://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
