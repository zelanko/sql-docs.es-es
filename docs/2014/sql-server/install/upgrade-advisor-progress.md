---
title: Progreso del Asesor de actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 697f70d4435213a991e55adecb51a98120d8df1b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091562"
---
# <a name="upgrade-advisor-progress"></a>Progreso del Asesor de actualizaciones
  El análisis del Asesor de actualizaciones se inicia con un analizador dedicado que realiza un análisis de cada componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seleccionó. A medida que se analizan los componentes, el progreso se muestra en el cuadro de diálogo de **progreso** .  
  
## <a name="options"></a>Opciones  
 **Acción**  
 Especifica el componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionado para el análisis.  
  
 **Estado**  
 Muestra el valor de estado devuelto desde la interfaz de progreso del componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Mensaje**  
 Muestra el mensaje de error o de confirmación que devuelve cada analizador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si el análisis se prolonga demasiado tiempo, puede detenerlo, salir del Asistente para análisis del Asesor de actualizaciones y, a continuación, volver a ejecutar el asistente. Para reducir el tiempo del análisis, seleccione menos componentes para analizar.  
  
 Cuando el análisis se haya completado, el informe se escribe en un archivo. Puede ver el informe haciendo clic en **iniciar Informe** para iniciar el visor de informes desde esta página. Si desea ver el informe más adelante, puede abrir el visor de **informes del Asesor de actualizaciones** desde la página de inicio del Asesor de actualizaciones.  
  
> [!NOTE]  
>  Los informes anteriores se guardan cada vez que se analice un servidor. Los informes se guardan con la marca de tiempo como nombre de archivo. El visor de informes muestra los cinco últimos informes guardados.  
  
## <a name="see-also"></a>Consulte también  
 [Cómo: iniciar el asesor de actualizaciones](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Cómo: ejecutar el Asistente para análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componentes de SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Referencia de la interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
