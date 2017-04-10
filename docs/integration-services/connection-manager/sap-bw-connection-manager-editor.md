---
title: "Editor del administrador de conexiones SAP BW | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sapbwconnectionmanager.f1"
ms.assetid: ec970319-e749-4753-8675-9cf76ed99669
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Editor del administrador de conexiones SAP BW
  Use el **Editor del administrador de conexiones de SAP BW** para especificar las propiedades que se van a usar para establecer una conexión con la versión 7 del sistema SAP Netweaver BW.  
  
 El administrador de conexiones de SAP BW aporta conectividad a cualquier sistema SAP Netweaver BW de la versión 7 que use el origen o destino de SAP BW. Para más información sobre el administrador de conexiones de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Administrador de conexiones de SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el Editor del administrador de conexiones de SAP BW**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el administrador de conexiones de SAP BW.  
  
2.  En el área Administradores de conexión, en la pestaña **Flujo de control** , lleve a cabo uno de los siguientes procedimientos:  
  
    -   Haga doble clic en administrador de conexiones de SAP BW.  
  
         O bien  
  
    -   Haga clic con el botón derecho en el administrador de conexiones de SAP BW y, después, seleccione **Editar**.  
  
## Opciones  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el administrador de conexiones, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 **Cliente**  
 Especifique el número de cliente del sistema.  
  
 **Lenguaje**  
 Permite especificar el idioma que usa el sistema. Por ejemplo, especifique **EN** para inglés.  
  
 **Nombre de usuario.**  
 Permite especificar el nombre de usuario que se va a utilizar para establecer la conexión al sistema.  
  
 **Contraseña**  
 Permite especificar la contraseña que se va a usar con el nombre de usuario.  
  
 **Usar un solo servidor de aplicaciones**  
 Permite conectarse a un único servidor de aplicaciones.  
  
 Para conectarse a un grupo de servidores con equilibrio de carga, use en su lugar la opción **Usar equilibrio de carga**.  
  
 **Host**  
 Si se va a conectar a un único servidor de aplicaciones, especifique el nombre de host.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar un solo servidor de aplicaciones**.  
  
 **Número del sistema**  
 Si se va a conectar a un único servidor de aplicaciones, especifique el número del sistema.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar un solo servidor de aplicaciones**.  
  
 **Usar equilibrio de carga**  
 Permite conectarse a un grupo de servidores con equilibrio de carga.  
  
 Para conectarse a un único servidor de aplicaciones, use en su lugar la opción **Usar un solo servidor de aplicaciones** .  
  
 **Servidor de Mensajería**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el nombre del servidor del mensaje.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga**.  
  
 **Grupo**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el nombre del grupo de servidores.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga**.  
  
 **SID**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el identificador del sistema para la conexión.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga**.  
  
 **Directorio de registro**  
 Permite habilitar el registro para los componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW.  
  
 Para habilitar el registro, debe especificar un directorio para los archivos de registro que se crean antes y después de cada llamada a funciones RFC. (Esta característica de registro crea múltiples archivos de registro en formato XML. Dado que estos archivos de registro también contienen todas las filas de datos que se transfieren, es posible que los archivos de registro consuman gran cantidad de espacio en disco).  
  
> [!IMPORTANT]  
>  Si los datos que se transfieren contienen información confidencial, los archivos de registro también contendrán esa información confidencial.  
  
 Para especificar el directorio de registro, puede escribir la ruta de acceso manualmente o bien, haga clic en **Examinar** y busque el directorio de registro.  
  
 Si no selecciona un directorio de registro, el registro no estará habilitado.  
  
 **Examinar**  
 Permite examinar para seleccionar una carpeta para el directorio de registro.  
  
 **Probar conexión**  
 Permite probar la conexión con los valores que ha especificado. Después de hacer clic en **Probar conexión**, aparecerá un cuadro de mensaje que indica si la conexión se realizó correctamente o no.  
  
## Vea también  
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  