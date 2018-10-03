---
title: Conectarse a una instancia desde el Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7947bba9f41ffb77a1260ce79a5f4afb6c773295
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110935"
---
# <a name="connect-to-an-instance-from-object-explorer"></a>Conectarse a una instancia desde el Explorador de objetos
  Para administrar objetos mediante el Explorador de objetos, primero debe conectarlo a la instancia que contiene los objetos. Puede conectar el Explorador de objetos a varias instancias simultáneamente.  
  
## <a name="connecting-object-explorer-to-a-server"></a>Conectar el Explorador de objetos a un servidor  
 Para utilizar el Explorador de objetos, primero es necesario conectarse a un servidor. Haga clic en **Conectar** en la barra de herramientas del Explorador de objetos y elija el tipo de servidor en la lista desplegable. Se abre el cuadro de diálogo **Conectar al servidor** . Para conectarse, debe proporcionar al menos el nombre del servidor y la información de autenticación correcta.  
  
## <a name="optional-object-explorer-connection-settings"></a>Valores de conexión opcionales del Explorador de objetos  
 Al conectarse a un servidor, es posible especificar información de conexión adicional en el cuadro de diálogo **Conectar al servidor** . El cuadro de diálogo **Conectar al servidor** conservará los últimos valores utilizados. Las nuevas conexiones, como las de las nuevas ventanas del Editor de código, utilizarán esos valores.  
  
 Para especificar valores de conexión opcionales, siga estos pasos:  
  
1.  Haga clic en **Conectar** en la barra de herramientas del Explorador de objetos y, a continuación, haga clic en el tipo de servidor al que desea conectarse. Aparece el cuadro de diálogo **Conectar al servidor** .  
  
2.  En el cuadro **Nombre del servidor** , escriba el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Haga clic en **Opciones**. El cuadro de diálogo **Conectar al servidor** mostrará opciones adicionales.  
  
4.  Haga clic en el pestaña **Propiedades de conexión** para definir los valores adicionales. Los valores disponibles varían según el tipo de servidor. En el [!INCLUDE[ssDE](../../includes/ssde-md.md)]están disponibles los valores siguientes.  
  
    |Parámetro|Descripción|  
    |-------------|-----------------|  
    |**Conectar con base de datos**|Se elige entre las bases de datos disponibles en el servidor. Esta lista solo mostrará las bases de datos que esté autorizado a ver.|  
    |**Protocolo de red**|Se selecciona entre Memoria compartida, TCP/IP o Canalizaciones con nombre.|  
    |**Tamaño del paquete de red**|Se configura en bytes. El valor predeterminado es 4096 bytes.|  
    |**Tiempo de espera de la conexión**|Se configura en segundos. El valor predeterminado es 15 segundos.|  
    |**Tiempo de espera de ejecución**|Se configura en segundos. El valor predeterminado (0) indica que el tiempo de espera de la ejecución nunca se agotará.|  
    |**Cifrar conexión**|Exige el uso de cifrado.|  
  
5.  Para agregar el servidor especificado a la lista de servidores registrados, haga clic en la pestaña **Servidor registrado** , haga clic en la ubicación en la que desea que aparezca el nuevo servidor y complete la conexión.  
  
> [!NOTE]  
>  Utilice la página **Parámetros de conexión adicionales** para agregar más parámetros de conexión a la cadena de conexión. Para más información, consulte [Conectar con el servidor &#40;Página Parámetros de conexión adicionales&#41;](../../database-engine/connect-to-server-additional-connection-parameters-page.md).  
  
  
