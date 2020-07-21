---
title: Intercalación de servidor Motor de base de datos incompatible (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 80f499d6-2c90-49eb-a5b3-0bb5b7faaa3b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c7a9df15948ddea5fe76efa1cce688f704cbe5c9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065372"
---
# <a name="incompatible-database-engine-server-collation-upgrade-advisor"></a>Intercalación del servidor de motor de base de datos incompatible (Asesor de actualizaciones)
  El asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que usa una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurada para utilizar una intercalación de servidor incompatible.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que usa una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que está configurada para utilizar una intercalación de servidor incompatible.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]El modo de SharePoint de emplea la arquitectura de servicios compartidos de SharePoint. SharePoint no admite [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] configurado para las intercalaciones de servidor o que distinguen entre mayúsculas y minúsculas o las intercalaciones de servidor binarias. Entre las intercalaciones incompatibles se incluyen las que son binarias o distinguen entre mayúsculas y minúsculas de forma predeterminada, y las intercalaciones base que son compatibles de forma predeterminada, pero se han configurado con alguno de los designadores de intercalación siguientes:  
  
-   **Binario**  
  
-   **Distinguir mayúsculas de minúsculas**  
  
-   **Punto de código binario**  
  
 Debido a que la intercalación de servidor actual de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] es incompatible, la actualización se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 La propiedad de intercalación del servidor de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no se puede cambiar. No podrá completar una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Deberá migrar la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un servidor nuevo que use una intercalación del servidor compatible. Para obtener más información, vea lo siguiente:  
  
-   [Actualizar y migrar Reporting Services](https://go.microsoft.com/fwlink/?LinkId=233227)  
  
-   [Seleccionar una intercalación de SQL Server](https://go.microsoft.com/fwlink/?LinkId=233226)  
  
  
