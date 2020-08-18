---
description: FTP, administrador de conexiones
title: Administrador de conexiones FTP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6aac44dfdbbe1c88965ff7aa37249651d3f7c199
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88350921"
---
# <a name="ftp-connection-manager"></a>FTP, administrador de conexiones

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un administrador de conexiones FTP habilita un paquete para conectarse a un servidor de Protocolo de transferencia de archivos (FTP). La tarea FTP que incluye [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa este administrador de conexiones.  
  
 Cuando agrega un Administrador de conexiones FTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un administrador de conexiones que se puede resolver como una conexión FTP en tiempo de ejecución, establece las propiedades del administrador de conexiones y agrega el administrador de conexiones a la colección **Connections** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **FTP**.  
  
 Puede configurar el administrador de conexiones FTP de las maneras siguientes:  
  
-   Especificar un nombre de servidor y puerto de servidor.  
  
-   Especificar un acceso anónimo, o proporcionar un nombre de usuario y una contraseña para la autenticación básica.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones FTP solo admite la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
-   Establecer el tiempo de espera, el número de reintentos y la cantidad de datos que se pueden copiar simultáneamente.  
  
-   Indicar si el administrador de conexiones FTP usa el modo pasivo o activo.  
  
 Según la configuración del sitio FTP al que se conecta el administrador de conexiones FTP, es posible que necesite cambiar los siguientes valores predeterminados del administrador de conexiones:  
  
-   El puerto del servidor se establece en 21. Debe especificar el puerto que escucha el sitio FTP.  
  
-   El nombre del usuario se establece en "anónimo". Debe proporcionar las credenciales que requiere el sitio FTP.  
  
## <a name="activepassive-modes"></a>Modos activo/pasivo  
 Un administrador de conexiones FTP puede enviar y recibir archivos con el modo activo o modo pasivo. En el modo activo, el servidor inicia la conexión de datos, mientras que en el modo pasivo, la inicia el cliente.  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>Configuración del administrador de conexiones FTP  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre las propiedades que se pueden configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="ftp-connection-manager-editor"></a>Editor del administrador de conexiones FTP
  Utilice el cuadro de diálogo **Editor del administrador de conexiones FTP** para especificar propiedades de conexión con un servidor FTP.  
  
> [!IMPORTANT]  
>  El administrador de conexiones FTP solo admite la autenticación anónima y la autenticación básica. No es compatible con la autenticación de Windows.  
  
 Para obtener más información acerca del administrador de conexiones FTP, vea [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Nombre del servidor**  
 Proporcione el nombre del servidor FTP.  
  
 **Puerto del servidor**  
 Especifique el número de puerto del servidor FTP que va a utilizar en la conexión. El valor predeterminado de esta propiedad es **21**.  
  
 **Nombre de usuario**  
 Indique un nombre de usuario para tener acceso al servidor FTP. El valor predeterminado de esta propiedad es **anonymous**.  
  
 **Contraseña**  
 Indique la contraseña para tener acceso al servidor FTP.  
  
 **Tiempo de espera (en segundos)**  
 Especifique el número de segundos que transcurrirán antes de que se exceda el tiempo de espera de la consulta. Si el valor es **0** , indica un período de tiempo infinito. El valor predeterminado de esta propiedad es **60**.  
  
 **Usar modo pasivo**  
 Especifique si inicia la conexión el servidor o el cliente. El servidor inicia la conexión en modo activo y el cliente en modo pasivo. El valor predeterminado de esta propiedad es **active mode**.  
  
 **Reintentos**  
 Especifique el número de veces que la tarea intenta establecer la conexión. Un valor de **0** indica que no existe límite en el número de intentos.  
  
 **Tamaño del fragmento (en KB)**  
 Indique un tamaño de fragmento en kilobytes para transmitir datos.  
  
 **Probar conexión**  
 Después de configurar el Administrador de conexiones FTP, haga clic en **Probar conexión**para confirmar que la conexión es viable.  
  
## <a name="see-also"></a>Vea también  
 [Tarea FTP](../../integration-services/control-flow/ftp-task.md)   
 [Conexiones de Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
