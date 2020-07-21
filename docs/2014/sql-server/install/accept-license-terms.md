---
title: Aceptar términos de licencia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 6d41879b84d98f72e570b00a61341a53d2e6187a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046449"
---
# <a name="accept-license-terms"></a>Aceptar los términos de licencia
  Use la página **Aceptar los términos de la licencia** del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de aceptar los términos de la licencia de esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede imprimir el contrato de licencia o copiarlo al Portapapeles. Para continuar, acepte los términos de licencia y, a continuación, haga clic en **Siguiente**. Para cerrar la instalación, haga clic en **Cancelar**.  
  
## <a name="customer-experience-improvement-program-ceip"></a>Programa para la mejora de la experiencia del usuario (CEIP)  
 Si habilita los informes del CEIP, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura para enviar periódicamente un informe a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Los informes incluyen información acerca de la configuración del hardware y de cómo se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los componentes. [!INCLUDE[msCoName](../../includes/msconame-md.md)] utilizará los datos de uso de características para mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entre los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que supervisa esta característica se incluyen los siguientes:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicación  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssNoVersion  
  
 La información sobre el uso de características se envía a [!INCLUDE[msCoName](../../includes/msconame-md.md)], donde se almacena limitando el acceso.  
  
 Para deshabilitar los informes del CEIP una vez completada la instalación, use la herramienta ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informes de uso y errores** del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] menú **herramientas de configuración** .  
  
 En el caso de acciones del programa de instalación como la instalación, actualización, reparación, etc., la información se recopila y se carga únicamente durante la ejecución del mismo  
  
 En el caso de los demás componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la información se recopila una vez al día para todas las instancias habilitadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, la hora de recopilación se establece en la medianoche para reducir la carga del servidor. Si desea cambiar la hora de recopilación, puede editar manualmente la clave del Registro que la controla. Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene su propia clave del Registro:  
  
 HKLM\Software \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<INSTANCEID> \CPE\TimeofReporting  
  
 El valor de esta clave del Registro contiene la hora de la recopilación que se va a ejecutar como número de minutos a partir de las 00:00 (medianoche). Por ejemplo, un valor de 60 ejecutaría la recopilación a la 1:00 a. m., un valor de 1200 ejecutaría la recopilación a las 8:00 p. m., etc.  
  
## <a name="error-reporting"></a>Informes de errores  
 Utilice la página **Configuración de informes de errores y uso** del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar la funcionalidad de informes de errores y de uso de las características en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opciones  
 De forma predeterminada, las características Recopilación de datos de uso de características e Informes de errores están deshabilitadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sus componentes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Informes de errores  
 Si habilita la característica Informes de errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura para enviar automáticamente un informe a [!INCLUDE[msCoName](../../includes/msconame-md.md)] si se produce un error irrecuperable en alguno de los siguientes componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Replicación  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] utiliza los informes de errores para mejorar la funcionalidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y trata toda la información recibida de forma confidencial.  
  
 La información sobre los errores se envía a través de una conexión segura (https) a [!INCLUDE[msCoName](../../includes/msconame-md.md)], donde se almacena con limitación de acceso. O bien, puede enviar los informes de errores a su propio servidor de informes de errores corporativo.  
  
 Los informes de errores contienen la información siguiente:  
  
-   La condición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el momento de producirse el problema.  
  
-   La versión del sistema operativo y del hardware del sistema.  
  
-   El identificador del producto digital, que puede utilizarse para identificar la licencia.  
  
-   La dirección IP de red del equipo o el servidor proxy.  
  
-   Información procedente de la memoria o los archivos del proceso que ha causado el error.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] no pretende obtener de forma intencionada archivos o información sobre el nombre, la dirección postal, la dirección de correo electrónico o información personal de otro tipo. Sin embargo, el informe de errores puede contener información personal procedente de la memoria o los archivos del proceso que ha causado el error. A pesar de que este tipo de información podría utilizarse potencialmente para determinar la identidad del usuario, [!INCLUDE[msCoName](../../includes/msconame-md.md)] no utiliza la información con este propósito.  
  
 Para obtener más información sobre la directiva de recopilación de datos y privacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea la [Declaración de privacidad de Microsoft SQL Server](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md).  
  
 Si habilita Informes de errores y se produce un error irrecuperable, podría ver en el registro de eventos de Windows una respuesta procedente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] que apunte a un artículo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base que trate sobre un error específico.  
  
 Para deshabilitar Informes de errores o Informes de uso de características en todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus componentes una vez finalizada la instalación, vaya al cuadro de diálogo **Configuración de informes de errores y uso** y desactive las casillas de **Uso de características**. Si el **Informe de errores** está habilitado para varios componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (,, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y componentes compartidos), puede deshabilitar los informes de errores para cada instancia de un componente individual, así como los componentes compartidos, que se enumeran como **otros**.  
  
## <a name="see-also"></a>Consulte también  
 [Acerca de los términos de licencia de SQL Server](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
