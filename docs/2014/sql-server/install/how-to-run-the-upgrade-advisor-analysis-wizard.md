---
title: 'Cómo: ejecutar el Asistente para análisis del Asesor de actualizaciones | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 548abb55ffcf6b8b0eca4ab7052a7995ef271a54
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059282"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Procedimientos: Ejecutar el Asistente para análisis del Asesor de actualizaciones
  Puede iniciar el Asistente para análisis del Asesor de actualizaciones desde la página de inicio de este último. En este tema se describe cómo ejecutar el Asistente para análisis del Asesor de actualizaciones.  
  
> [!IMPORTANT]
>  Cuando ejecute el Asistente para análisis del Asesor de actualizaciones, el Asesor de actualizaciones guarda los informes en la carpeta predeterminada para informes. No obstante, el visor de informes solo muestra los cinco últimos informes guardados. La ubicación predeterminada de los informes es la actualización de mis documentos \\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Advisor\110\Reports.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Para ejecutar el Asistente para análisis del Asesor de actualizaciones  
  
1.  En la página de inicio del Asesor de actualizaciones, haga clic en **iniciar el Asistente para análisis del Asesor de actualizaciones**.  
  
2.  En la página ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes** , escriba el nombre del servidor que se va a examinar en el cuadro **nombre del servidor** y, a continuación, haga clic en **detectar**. Siga las instrucciones que se detallan a continuación para especificar el nombre del servidor:  
  
    -   Para examinar instancias no agrupadas, escriba el nombre del equipo.  
  
    -   Para examinar instancias en clúster, escriba el nombre virtual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Para examinar los componentes no agrupados que están instalados en un nodo de un clúster, escriba el nombre del nodo.  
  
    > [!WARNING]  
    >  El Asesor de actualizaciones no admite la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no configurada para usar el puerto estándar (1433) para las conexiones de clientes. Si desea establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no usa el puerto estándar (1433), cree un alias mediante la dirección IP y el puerto. Para obtener más información sobre cómo configurar los protocolos de cliente y crear un alias para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las instancias, vea [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Si no tiene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo en el que está ejecutando el asesor de actualizaciones, haga clic en **Inicio**y, a continuación, en ejecutar `cliconfg` . Se abrirá el cuadro de diálogo ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramienta de red de cliente** . Use la pestaña **alias** para crear el alias.  
  
3.  Revise la lista de componentes detectados, modifique las selecciones según sea necesario y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **parámetros de conexión** , seleccione la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea examinar, seleccione el método de autenticación y, si es necesario, escriba la información de nombre de usuario y contraseña y, a continuación, haga clic en **siguiente**.  
  
     El nombre de instancia predeterminado es MSSQLSERVER.  
  
5.  Para los componentes seleccionados, escriba la información solicitada. Para obtener más información sobre los cuadros de diálogo individuales, vea referencia de la [interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  En la página **confirmar configuración del Asesor de actualizaciones** , revise la información que ha escrito. Puede seleccionar **enviar informes a [!INCLUDE[msCoName](../../includes/msconame-md.md)] ** si desea enviar el informe de actualización. También puede revisar la directiva de privacidad.  
  
7.  Haga clic en **Ejecutar** para analizar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
8.  Una vez finalizado el análisis, haga clic en **iniciar Informe** para ver los problemas detectados de la actualización.  
  
## <a name="see-also"></a>Consulte también  
 [Cómo: iniciar el asesor de actualizaciones](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Ejecutar el asesor de actualizaciones &#40;interfaz de usuario&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
