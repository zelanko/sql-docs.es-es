---
title: 'rsModelGenerationError: error de Reporting Services | Microsoft Docs'
description: 'En esta página de referencia de error, obtenga información sobre el identificador de evento "rsModelGenerationError": Error al generar el modelo.'
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfeb477ac1830d9604e3d794e96e807548639671
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487254"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Error de Reporting Services
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Id. de evento|rsRenderingError|  
|Origen de eventos|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|Error al generar el modelo. (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>Explicación  
 No se puede generar el modelo de informe. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 SP1 y en versiones anteriores, es más probable que se muestre este error cuando el objeto System.Data.DataSet no puede controlar una tabla o relación del esquema de la base de datos, como cuando, por ejemplo, se definen dos claves externas para la misma columna de una tabla.  
  
## <a name="user-action"></a>Acción del usuario  
 Para determinar el motivo específico por el que aparece este mensaje de error, revise los archivos de registro del servidor de informes, que se encuentran en \Microsoft SQL Server\\<Instancia de SQL Server\>\Reporting Services\LogFiles.  
  
## <a name="internal-only"></a>Solo para uso interno  
  
