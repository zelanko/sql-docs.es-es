---
title: 'Cómo: ejecutar el Asistente para análisis del Asesor | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
caps.latest.revision: 36
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29aeaa20d5fed63731c84872ffb193da4bcfce27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282571"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Cómo: ejecutar el Asistente para análisis del Asesor
  Puede iniciar el Asistente para análisis del Asesor de actualizaciones desde la página de inicio de este último. En este tema se describe cómo ejecutar el Asistente para análisis del Asesor de actualizaciones.  
  
> [!IMPORTANT]  
>  Cuando ejecute el Asistente para análisis del Asesor de actualizaciones, el Asesor de actualizaciones guarda los informes en la carpeta predeterminada para informes. No obstante, el visor de informes solo muestra los cinco últimos informes guardados. La ubicación predeterminada para los informes es Mis documentos\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Para ejecutar al Asistente para actualización de análisis de Advisor  
  
1.  En la página de inicio del Asesor de actualizaciones, haga clic en **iniciar Asistente de análisis del Asistente para actualizar**.  
  
2.  En el  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes** , escriba el nombre del servidor para examinar en el **nombre del servidor** cuadro y, a continuación, haga clic en **detectar**. Siga las instrucciones que se detallan a continuación para especificar el nombre del servidor:  
  
    -   Para examinar instancias que no estén en clúster, escriba el nombre del equipo.  
  
    -   Para examinar instancias en clúster, escriba el nombre virtual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Para examinar componentes no clúster instalados en el nodo de un clúster, escriba el nombre del nodo.  
  
    > [!WARNING]  
    >  El Asesor de actualizaciones no admite la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no configurada para usar el puerto estándar (1433) para las conexiones de clientes. Si desea establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no usa el puerto estándar (1433), cree un alias mediante la dirección IP y el puerto. Para obtener más información sobre cómo configurar protocolos de cliente y crear un alias para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancias, consulte [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Si no tienes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo en el que se ejecuta el Asesor de actualizaciones, haga clic en **iniciar**y, a continuación, ejecute `cliconfg`. Se abrirá el  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramienta de red de cliente** cuadro de diálogo. Use la **Alias** pestaña para crear el alias.  
  
3.  Revise la lista de componentes detectados, modifique las selecciones según sea necesario y, a continuación, haga clic en **siguiente**.  
  
4.  En el **parámetros de conexión** , seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desea examinar, seleccione el método de autenticación y, si es necesario, escriba la información de nombre y la contraseña de usuario y, a continuación, haga clic en **siguiente**.  
  
     El nombre de instancia predeterminado es MSSQLSERVER.  
  
5.  Para los componentes seleccionados, escriba la información solicitada. Para obtener más información sobre los diferentes cuadros de diálogo, vea [Actualizar referencia de interfaz de usuario del Asistente para](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  En el **Confirmar configuración del Asistente para actualización** página, revise la información que ha escrito. Puede seleccionar **enviar informes a [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  si desea enviar el informe de actualización. También puede revisar la directiva de privacidad.  
  
7.  Haga clic en **ejecutar** para analizar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
8.  Cuando finalice el análisis, haga clic en **iniciar informe** para ver los problemas de actualización detectados.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: iniciar el Asesor de actualizaciones](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Ejecute el Asesor de actualizaciones &#40;interfaz de usuario&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
