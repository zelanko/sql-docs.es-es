---
description: Administrador de conexiones de SAP BW
title: Administrador de conexiones de SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a67889df1635e2654adc80151e33a1c137985d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426007"
---
# <a name="sap-bw-connection-manager"></a>Administrador de conexiones de SAP BW

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El administrador de conexiones de SAP BW es el componente del administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Por tanto, el administrador de conexiones de SAP BW proporciona conectividad a un sistema SAP Netweaver BW versión 7 que necesitan los componentes de destino y de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. (El origen y el destino de SAP BW que forman parte del paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW son los únicos componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que usan el administrador de conexiones de SAP BW).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 Cuando agrega un administrador de conexiones de SAP BW a un paquete, la propiedad **ConnectionManagerType** del administrador de conexiones se establece en **SAPBI**.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Configurar el administrador de conexiones de SAP BW  
 Puede configurar el administrador de conexiones de SAP BW de las maneras siguientes:  
  
-   Facilite el cliente, el nombre de usuario, la contraseña y el idioma de la conexión.  
  
-   Elija si desea conectarse a un único servidor de aplicaciones o un grupo de servidores con equilibrio de carga.  
  
-   Proporcione el número de host y del sistema para un único servidor de aplicaciones o proporcione el servidor de mensajes, grupo y SID de un grupo de servidores con equilibrio de carga.  
  
-   Habilite el registro personalizado de llamadas a funciones RFC para los componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. (Este registro es independiente del registro opcional que puede habilitar en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ). Para habilitar el registro de las llamadas a funciones RFC, debe especificar un directorio en el que almacenar los archivos de registro que se crean antes y después de cada llamada a funciones RFC. (Esta característica de registro crea múltiples archivos de registro en formato XML. Dado que estos archivos de registro también contienen todas las filas de datos que se transfieren, es posible que los archivos de registro consuman gran cantidad de espacio en disco). Si no selecciona un directorio de registro, el registro no estará habilitado.  
  
    > [!IMPORTANT]  
    >  Si los datos que se transfieren contienen información confidencial, los archivos de registro también contendrán esa información confidencial.  
  
-   Use los valores especificados para probar la conexión.  
  
 Si no conoce todos los valores necesarios para configurar el administrador de conexiones, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 Para obtener instrucciones sobre cómo configurar y utilizar el administrador de conexiones, el origen y el destino de SAP BW, vea las notas del producto, [Usar SQL Server 2008 Integration Services con SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Estas notas del producto también muestran cómo configurar los objetos necesarios en SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usar el Diseñador SSIS para configurar el origen  
 Para obtener más información sobre las propiedades del administrador de conexiones de SAP BW que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Editor del administrador de conexiones SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md)  
  
## <a name="sap-bw-connection-manager-editor"></a>Editor del administrador de conexiones SAP BW
  Use el **Editor del administrador de conexiones de SAP BW** para especificar las propiedades que se van a usar para establecer una conexión con la versión 7 del sistema SAP Netweaver BW.  
  
 El administrador de conexiones de SAP BW aporta conectividad a cualquier sistema SAP Netweaver BW de la versión 7 que use el origen o destino de SAP BW. Para más información sobre el administrador de conexiones de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Administrador de conexiones de SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el Editor del administrador de conexiones de SAP BW**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el administrador de conexiones de SAP BW.  
  
2.  En el área Administradores de conexión, en la pestaña **Flujo de control** , lleve a cabo uno de los siguientes procedimientos:  
  
    -   Haga doble clic en administrador de conexiones de SAP BW.  
  
         o bien  
  
    -   Haga clic con el botón derecho en el administrador de conexiones de SAP BW y, después, seleccione **Editar**.  
  
### <a name="options"></a>Opciones  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el administrador de conexiones, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 **Cliente**  
 Especifique el número de cliente del sistema.  
  
 **Lenguaje**  
 Permite especificar el idioma que usa el sistema. Por ejemplo, especifique **EN** para inglés.  
  
 **Nombre de usuario**  
 Permite especificar el nombre de usuario que se va a utilizar para establecer la conexión al sistema.  
  
 **Contraseña**  
 Permite especificar la contraseña que se va a usar con el nombre de usuario.  
  
 **Usar un solo servidor de aplicaciones**  
 Permite conectarse a un único servidor de aplicaciones.  
  
 Para conectarse a un grupo de servidores con equilibrio de carga, use en su lugar la opción **Usar equilibrio de carga** .  
  
 **Host**  
 Si se va a conectar a un único servidor de aplicaciones, especifique el nombre de host.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar un solo servidor de aplicaciones** .  
  
 **Número del sistema**  
 Si se va a conectar a un único servidor de aplicaciones, especifique el número del sistema.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **Usar un solo servidor de aplicaciones** .  
  
 **Usar equilibrio de carga**  
 Permite conectarse a un grupo de servidores con equilibrio de carga.  
  
 Para conectarse a un único servidor de aplicaciones, use en su lugar la opción **Usar un solo servidor de aplicaciones** .  
  
 **Servidor de mensajes**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el nombre del servidor del mensaje.  
  
> [!NOTE]  
>   Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga** .  
  
 **Grupo**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el nombre del grupo de servidores.  
  
> [!NOTE]  
>   Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga** .  
  
 **SID**  
 Si se conecta a un grupo de servidores con equilibrio de carga, especifique el identificador del sistema para la conexión.  
  
> [!NOTE]  
>   Esta opción solo está disponible si ha seleccionado la opción **Usar equilibrio de carga** .  
  
 **Directorio de registro**  
 Permite habilitar el registro para los componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW.  
  
 Para habilitar el registro, debe especificar un directorio para los archivos de registro que se crean antes y después de cada llamada a funciones RFC. (Esta característica de registro crea múltiples archivos de registro en formato XML. Dado que estos archivos de registro también contienen todas las filas de datos que se transfieren, es posible que los archivos de registro consuman gran cantidad de espacio en disco).  
  
> [!IMPORTANT]  
>  Si los datos que se transfieren contienen información confidencial, los archivos de registro también contendrán esa información confidencial.  
  
 Para especificar el directorio de registro, puede escribir la ruta de acceso manualmente o bien, haga clic en **Examinar** y busque el directorio de registro.  
  
 Si no selecciona un directorio de registro, el registro no estará habilitado.  
  
 **Browse**  
 Permite examinar para seleccionar una carpeta para el directorio de registro.  
  
 **Probar conexión**  
 Permite probar la conexión con los valores que ha especificado. Después de hacer clic en **Probar conexión**, aparecerá un cuadro de mensaje que indica si la conexión se realizó correctamente o no.  
  
## <a name="see-also"></a>Consulte también  
 [Componentes de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
