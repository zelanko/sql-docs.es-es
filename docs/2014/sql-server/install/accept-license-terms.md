---
title: Acepte los términos de licencia | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 55d500b13cc3ab3c859474bb3050e29a7487f4a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204084"
---
# <a name="accept-license-terms"></a>Aceptar los términos de licencia
  Use la **Aceptar los términos de licencia** página de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación para aceptar los términos de licencia para esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede imprimir el contrato de licencia o copiarlo al Portapapeles. Para continuar, acepte los términos de licencia y, a continuación, haga clic en **Siguiente**. Para cerrar la instalación, haga clic en **Cancelar**.  
  
## <a name="customer-experience-improvement-program-ceip"></a>Programa para la mejora de la experiencia del usuario (CEIP)  
 Si habilita los informes del CEIP, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura para enviar periódicamente un informe a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Los informes incluyen información acerca de la configuración del hardware y de cómo se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los componentes. [!INCLUDE[msCoName](../../includes/msconame-md.md)] utilizará los datos de uso de características para mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entre los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que supervisa esta característica se incluyen los siguientes:  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   REPLICATION  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Programa de instalación  
  
 Información sobre el uso de características se envía a [!INCLUDE[msCoName](../../includes/msconame-md.md)], donde se almacena con acceso limitado.  
  
 Para deshabilitar los informes del CEIP una vez completada la instalación, utilice la  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informes de errores y uso** herramienta en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **herramientas de configuración** menú.  
  
 En el caso de acciones del programa de instalación como la instalación, actualización, reparación, etc., la información se recopila y se carga únicamente durante la ejecución del mismo  
  
 En el caso de los demás componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la información se recopila una vez al día para todas las instancias habilitadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, la hora de recopilación se establece en la medianoche para reducir la carga del servidor. Si desea cambiar la hora de recopilación, puede editar manualmente la clave del Registro que la controla. Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene su propia clave del registro:  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< INSTANCEID > \CPE\TimeofReporting  
  
 El valor de esta clave del Registro contiene la hora de la recopilación que se va a ejecutar como número de minutos a partir de las 00:00 (medianoche). Por ejemplo, un valor de 60 ejecutaría la recopilación a la 1:00 a. m., un valor de 1200 ejecutaría la recopilación a las 8:00 p. m., etc.  
  
## <a name="error-reporting"></a>Informes de errores  
 Use la **configuración de informes de uso y errores** página de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación para habilitar para la funcionalidad de informes de uso y errores de la característica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="options"></a>Opciones  
 De forma predeterminada, la recopilación de datos de uso de las características y funciones de informe de errores están deshabilitadas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus componentes en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Informes de errores  
 Si habilita la característica informe de errores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para enviar un informe a [!INCLUDE[msCoName](../../includes/msconame-md.md)] automáticamente si se produce un error irrecuperable en alguno de los siguientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes:  
  
-   El [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   REPLICATION  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] utiliza los informes de errores para mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionalidad y trata toda la información de forma confidencial.  
  
 La información sobre los errores se envía a través de una conexión segura (https) a [!INCLUDE[msCoName](../../includes/msconame-md.md)], donde se almacena con limitación de acceso. O bien, puede enviar los informes de errores a su propio servidor de informes de errores corporativo.  
  
 Los informes de errores contienen la información siguiente:  
  
-   La condición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se produjo el problema.  
  
-   La versión del sistema operativo y del hardware del sistema.  
  
-   El identificador del producto digital, que puede utilizarse para identificar la licencia.  
  
-   La dirección IP de red del equipo o el servidor proxy.  
  
-   Información procedente de la memoria o los archivos del proceso que ha causado el error.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] no recopila intencionadamente los archivos, nombre, dirección, dirección de correo electrónico o cualquier otra forma de información personal. Sin embargo, el informe de errores puede contener información personal procedente de la memoria o los archivos del proceso que ha causado el error. A pesar de que este tipo de información podría utilizarse potencialmente para determinar la identidad del usuario, [!INCLUDE[msCoName](../../includes/msconame-md.md)] no utiliza la información con este propósito.  
  
 Para obtener más información sobre la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] privacidad y la directiva de recopilación de datos, vea [declaración de privacidad de Microsoft SQL Server](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md).  
  
 Si habilita Informes de errores y se produce un error irrecuperable, podría ver en el registro de eventos de Windows una respuesta procedente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] que apunte a un artículo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base que trate sobre un error específico.  
  
 Para deshabilitar informe de errores o uso de características para todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus componentes una vez completada la instalación, vaya a la **configuración de informes de uso y errores** cuadro de diálogo y desactive las casillas de verificación para **uso de características** . Si **informe de errores de** está habilitado para varios componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y componentes compartidos) puede deshabilitar informe de errores para cada instancia de un usuario individual componente, así como los componentes compartidos, que aparece como **otros**.  
  
## <a name="see-also"></a>Vea también  
 [Acerca de los términos de licencia SQL Server](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  