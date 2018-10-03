---
title: (Servidor de informes de modo nativo) de la implementación escalada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.scaleoutdeployment.F1
ms.assetid: 4df38294-6f9d-4b40-9f03-1f01c1f0700c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c091c115f9e03fbc0f1243e1c2fcf3a075f3586f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099945"
---
# <a name="scale-out-deployment-native-mode-report-server"></a>Implementación escalada horizontalmente (servidor de informes en modo nativo)
  Use la **implementación escalada** página [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para ver el estado de inicialización para una implementación escalada o para unir un servidor de informes a una implementación escalada. *Implementación escalada* se refiere a dos o más instancias de un servidor de informes que comparten una sola base de datos de servidor de informes.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Un *servidor de informes inicializado* describe un servidor que puede cifrar y descifrar datos confidenciales que se almacenan en una base de datos del servidor de informes (las credenciales almacenadas y las cadenas de conexión son ejemplos de datos cifrados que se almacenan en la base de datos). La inicialización del servidor de informes es un requisito para las operaciones del servidor de informes.  
  
 Una *implementación escalada* se usa en los escenarios siguientes:  
  
-   Como requisito previo para lograr el equilibrio de carga en varios servidores de informes de un clúster de servidores. Para poder equilibrar la carga en varios servidores de informes, debe configurarlos primero de modo que compartan la misma base de datos.  
  
-   Para segmentar las aplicaciones del servidor de informes en equipos diferentes mediante el uso de un servidor para el procesamiento interactivo de los informes y de un segundo servidor para el procesamiento programado de los informes. En este escenario, cada instancia del servidor procesa tipos diferentes de solicitudes para el contenido del mismo servidor de informes que se almacena en la base de datos compartida.  
  
 Para configurar una implementación escalada, comience conectando una o más instancias del servidor de informes a la misma base de datos. Una vez instaladas todas las instancias, conéctese al primer servidor de informes y, a continuación, use la página Implementación escalada para unir cada instancia adicional. Solo un servidor de informes que ya se haya inicializado para utilizar una base de datos puede inicializar nodos adicionales.  
  
 Para abrir esta página, inicie el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager y seleccione **implementación escalada** en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de SQL Server**  
 Especifique el nombre de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia que hospeda la base de datos del servidor de informes.  
  
 **Database Name**  
 Especifica el nombre de la base de datos a la que está conectada actualmente la instancia del servidor de informes.  
  
 **Modo de servidor**  
 Muestra el modo de servidor y la base de datos. El modo de servidor es o bien nativo o bien integrado de SharePoint. Las implementaciones escaladas se admiten en ambos modos.  
  
 **Server**  
 Muestra el nombre del servidor de informes. En la mayor parte de los casos, éste es el nombre del equipo en el que se instala el servidor de informes.  
  
 **Instancia**  
 Muestra el nombre de la instancia del servidor de informes. Las instancias del servidor de informes se basan en las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Estado**  
 Indica si el servidor de informes está inicializado o esperando para unirse a una implementación escalada:  
  
-   En un servidor de informes independiente que no forme parte de una implementación escalada, esta página muestra que la instancia del servidor de informes está inicializada con respecto a su base de datos dedicada. El estado está establecido en **Combinados**.  
  
-   En un servidor de informes que esté esperando unirse a una implementación escalada, esta página contiene valores vacíos en Servidor, Instancia y Estado. Un servidor de informes está esperando para unirse una implementación escalada si se seleccionó una base de datos de servidor de informes existente que otra instancia del servidor de informes ya esté usando. Un mensaje en esta página le indica que se conecte a un servidor de informes que ya está unido a la granja de servidores. Para completar esta solicitud, haga clic en **Conectar**, seleccione un servidor de informes que ya esté inicializado para utilizar la base de datos del servidor de informes, haga clic en **Implementación escalada**, seleccione la instancia del servidor de informes que esté **Esperando para unirse**y, a continuación, haga clic en **Inicializar**.  
  
-   Para un servidor de informes que forme parte actualmente de una implementación escalada, esta página muestra el estado de inicialización de todas las instancias del servidor de informes que comparten la misma base de datos del servidor de informes. Cuando se visualiza el estado de una implementación escalada, no importa a qué servidor se está conectado. La información del estado se notifica de forma idéntica para todos los nodos de la implementación escalada.  
  
     En un servidor de informes que ya forme parte de una implementación escalada, puede utilizar esta página para agregar o quitar nodos.  
  
 **inicializar**  
 Haga clic en **Inicializar** para agregar un servidor de informes a la implementación escalada. Este paso permite configurar un servidor de informes para usar una clave simétrica en una base de datos de servidor de informes compartida. Utilice la opción **Inicializar** para agregar una instancia del servidor de informes a una implementación de ampliación horizontal.  
  
 Una instancia del servidor de informes está disponible solo si se ha configurado previamente una conexión con la base de datos compartida del servidor de informes. Además, debe realizar la inicialización desde un servidor de informes ya inicializado para utilizar la base de datos del servidor de informes.  
  
 **Quitar**  
 Haga clic en **Quitar** para quitar las claves de cifrado de la instancia del servidor de informes de la base de datos del servidor de informes. Puede quitar claves para quitar una instancia del servidor de informes de una implementación de ampliación horizontal o para solucionar un problema de migración o instalación. Con esta opción, solo se quitan las claves de cifrado para la instancia del servidor de informes especificada. Esto no afecta a los datos cifrados de la base de datos del servidor de informes.  
  
 Como precaución, asegúrese de crear una copia de seguridad de la clave simétrica antes de quitarla. Una vez que haya quitado las claves de cifrado del último servidor de informes de la lista, especifique los nuevos requisitos para la siguiente inicialización del servidor de informes para dicha base de datos. El nuevo requisito es que, tras inicializar un servidor de informes, debe restaurar una copia de seguridad de la clave simétrica. La restauración de la clave simétrica es necesaria si desea tener acceso a los datos cifrados alojados actualmente en la base de datos del servidor de informes.  
  
 Si ya no necesita los datos cifrados o si no tiene una copia de seguridad de la clave, debe eliminar los datos cifrados. Para obtener más información, consulte [las claves de cifrado &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
