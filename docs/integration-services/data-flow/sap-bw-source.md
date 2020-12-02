---
description: Origen de SAP BW
title: Origen de SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8d62e20117bf23511a1d261142a3618dcbd5095a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "92195337"
---
# <a name="sap-bw-source"></a>Origen de SAP BW

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El origen de SAP BW es el componente de origen de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Así, el origen de SAP BW extrae datos de un sistema SAP Netweaver BW de la versión 7 y hace que estos datos estén disponibles para el flujo de datos en un paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Este origen tiene una salida y una salida de error.  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
 Para usar un origen de SAP BW, deberá realizar las tareas siguientes:  
  
-   [Preparar los objetos de SAP Netweaver BW](#bkmk_Prepare_Objects)  
  
-   [Conectarse al sistema SAP Netweaver BW](#bkmk_Connect_Database)  
  
-   [Configurar el origen de SAP BW](#bkmk_Configure_Source)  
  
##  <a name="preparing-the-sap-netweaver-bw-objects-that-the-source-requires"></a><a name="bkmk_Prepare_Objects"></a> Preparar los objetos SAP Netweaver BW que requiera el origen  
 El origen de SAP BW requiere que ciertos objetos estén en el sistema SAP Netweaver BW antes de que pueda funcionar el origen. Si estos objetos no existen aún, debe seguir estos pasos para crear y configurar estos objetos en el sistema SAP Netweaver BW.  
  
> [!NOTE]  
>  Para obtener detalles adicionales sobre estos objetos y pasos de configuración, vea la documentación sobre SAP Netweaver BW.  
  
1.  Inicie sesión en SAP Netweaver BW MDX a través de la GUI de SAP, escriba el código SM59 de transacciones y cree un destino RFC:  
  
    1.  Para **Tipo de conexión**, seleccione **TCP/IP**.  
  
    2.  Para **Tipo de activación**, seleccione **Programa de servidor registrado**.  
  
    3.  Para **Tipo de comunicación con sistema de destino**, seleccione **No Unicode (valores inactivos de MDMP)**.  
  
    4.  Asignar un identificador de programa adecuado  
  
2.  Crear un destino de concentrador abierto:  
  
    1.  Vaya al área de trabajo del administrador (código de transacción RSA1) y, en el panel izquierdo, seleccione **Open Hub Destination**(Destino de concentrador abierto).  
  
    2.  En el panel central, haga clic con el botón derecho en un elemento InfoArea y, después, seleccione **Create Open Hub Destination**(Crear destino de concentrador abierto).  
  
    3.  Para **Tipo de destino**, seleccione **“Herramienta de terceros”** y, a continuación, especifique el destino RFC que había creado anteriormente.  
  
    4.  Guarde y active el nuevo destino de concentrador abierto.  
  
3.  Cree un proceso de transferencia de datos (DTP):  
  
    1.  En el panel central del elemento InfoArea, haga clic con el botón derecho en el destino que creó anteriormente y, después, seleccione **Create data transfer process**(Crear proceso de transferencia de datos).  
  
    2.  Configure, guarde y active el DTP.  
  
    3.  En el menú, haga clic en **Ir a** y, a continuación, haga clic en **Configuración del administrador de lotes**.  
  
    4.  Actualice **Número de procesos** a 1 para el procesamiento en serie.  
  
4.  Cree una cadena de procesos:  
  
    1.  Al configurar la cadena de procesos, seleccione **Comenzar a usar cadena de metadatos o API** como las **Opciones de programación** del **Proceso de inicio** y, a continuación, agregue el DTP que había creado anteriormente como nodo subsiguiente.  
  
    2.  Guarde y active la cadena de procesos.  
  
     El origen de SAP BW puede llamar a la cadena de procesos para activar el proceso de transferencia de datos.  
  
##  <a name="connecting-to-the-sap-netweaver-bw-system"></a><a name="bkmk_Connect_Database"></a> Conectarse al sistema SAP Netweaver BW  
 Para conectarse al sistema SAP Netweaver BW de la versión 7, el origen de SAP BW usa un administrador de conexiones para SAP BW que forma parte del paquete [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. El administrador de conexiones de SAP BW es el único administrador de conexiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que puede usar el origen de SAP BW.  
  
 Para obtener más información sobre el administrador de conexiones de SAP BW, vea [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="configuring-the-sap-bw-source"></a><a name="bkmk_Configure_Source"></a> Configurar el origen de SAP BW  
 Puede configurar el origen de SAP BW de las maneras siguientes:  
  
-   Busque y seleccione el destino del servicio de concentrador abierto (OHS) que se usará para extraer datos.  
  
-   Seleccione uno de los métodos siguientes para extraer datos:  
  
    -   Desencadene una cadena de procesos. En este caso, el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inicia el proceso de extracción.  
  
    -   Espere a recibir la notificación del sistema SAP Netweaver BW para comenzar una extracción. En este caso, el sistema SAP Netweaver BW inicia el proceso de extracción.  
  
    -   Recupere los datos asociados a un identificador de solicitud determinado. En este caso, el sistema SAP Netweaver BW ha extraído ya los datos a una tabla interna y el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solo lee los datos.  
  
-   En función del método seleccionado para extraer datos, proporcione la información adicional siguiente:  
  
    -   Para la opción **P - Desencadenar cadena de procesos** , proporcione el nombre de host de puerta de enlace, el nombre del servicio de la puerta de enlace, el identificador de programa para el destino RFC y el nombre de la cadena de procesos.  
  
    -   Para la opción **W - Esperar notificación** , proporcione el nombre de host de puerta de enlace, el nombre del servidor de la puerta de enlace y el identificador de programa para el destino de RFC. Asimismo, puede especificar el tiempo de espera (en segundos). El tiempo de espera es el periodo de tiempo máximo que esperará el origen para recibir la notificación.  
  
    -   Para la opción **E - Extraer únicamente** , proporcione el identificador de solicitud.  
  
-   Especifique las reglas de conversión de cadenas. (Por ejemplo, convierta todas las cadenas en función de si el sistema SAP Netweaver BW es Unicode o no, o convierta todas las cadenas a **varchar** o **nvarchar**).  
  
-   Use las opciones que ha seleccionado para obtener una vista previa de los datos que se van a extraer.  
  
 También puede habilitar el registro de las llamadas del origen a funciones RFC. (Este registro es independiente del registro opcional que puede habilitar en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ). Las llamadas a funciones RFC se habilitan cuando se configura el administrador de conexiones SAP BW que va a usar el origen. Para obtener más información sobre cómo configurar el administrador de conexiones de SAP BW, vea [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Si no conoce todos los valores necesarios para configurar el origen, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 Para obtener instrucciones sobre cómo configurar y utilizar el administrador de conexiones, el origen y el destino de SAP BW, vea las notas del producto, [Usar SQL Server 2008 Integration Services con SAP BI 7.0](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100)). Estas notas del producto también muestran cómo configurar los objetos necesarios en SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usar el Diseñador SSIS para configurar el origen  
 Para obtener más información sobre las propiedades del origen de SAP BW que puede establecer en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de SAP BW &#40;página Columnas&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)  
  
-   [Editor de origen de SAP BW &#40;página Salida de error&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)  
  
-   [Editor de origen de SAP BW &#40;página Opciones avanzadas&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)  
  
 Mientras configura el origen de SAP BW, también puede usar varios cuadros de diálogo para buscar los objetos de SAP Netweaver BW o para obtener una vista previa de los datos de origen. Para obtener más información sobre estos cuadros de diálogo, haga clic en uno de los temas siguientes:  
  
-   [Buscar destino RFC](../../integration-services/data-flow/look-up-rfc-destination.md)  
  
-   [Buscar cadena de procesos](../../integration-services/data-flow/look-up-process-chain.md)  
  
-   [Registro de solicitudes](../../integration-services/data-flow/request-log.md)  
  
-   [Versión preliminar](../../integration-services/data-flow/preview.md)  
  
## <a name="see-also"></a>Vea también  
 [Componentes de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
