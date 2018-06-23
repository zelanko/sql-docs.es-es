---
title: Opciones (SQL Server AlwaysOn, página de panel) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 553f76520f9bb292d795fbbd5e13833391d6bdab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196520"
---
# <a name="options-sql-server-alwayson-dashboard-page"></a>Opciones (SQL Server AlwaysOn, página del panel)
  Use la página **Panel AlwaysOn de SQL Server** del cuadro de diálogo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**de** para configurar el panel AlwaysOn.  
  
 **Para acceder a esta página:**  
  
 En el menú **Herramientas** , haga clic en **Opciones**, expanda la carpeta **SQL Server AlwaysOn** y, a continuación, haga clic en **Panel**.  
  
## <a name="on-this-page"></a>En esta página  
 **Activar actualización automática.**  
 Haga clic para habilitar la actualización automática. Las opciones son:  
  
-   El campo **Intervalo de actualización (en segundos)** muestra el número de segundos que pasarán antes de cada actualización del panel. El valor predeterminado es 30. Cuando se habilita la actualización automática, se puede editar este campo para cambiar el intervalo de actualización.  
  
-   El **Número de reintentos de conexión** muestra el número de veces que el panel intentará conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda una réplica de disponibilidad para un grupo de disponibilidad que el panel está supervisando. El valor predeterminado es 65535. Cuando se habilita la actualización automática, se puede editar este campo para cambiar el número de reintentos de conexión.  
  
 **Habilitar la directiva de AlwaysOn definida por el usuario.**  
 Si ha definido su propia directiva de AlwaysOn, haga clic en esta opción para habilitar su directiva.  
  
## <a name="see-also"></a>Vea también  
 [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  