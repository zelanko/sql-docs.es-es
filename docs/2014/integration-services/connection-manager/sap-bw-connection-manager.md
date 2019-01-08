---
title: Administrador de conexiones de SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbff810eadb2a070cc6df7dec6985e21f50e9eb4
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369717"
---
# <a name="sap-bw-connection-manager"></a>Administrador de conexiones de SAP BW
  El administrador de conexiones de SAP BW es el componente del administrador de conexiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Por tanto, el administrador de conexiones de SAP BW proporciona conectividad a un sistema SAP Netweaver BW versión 7 que necesitan los componentes de destino y de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. (El origen y el destino de SAP BW que forman parte del paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW son los únicos componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que usan el administrador de conexiones de SAP BW).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 Cuando agrega un administrador de conexiones de SAP BW a un paquete, la propiedad `ConnectionManagerType` del administrador de conexiones se establece en `SAPBI`.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Configurar el administrador de conexiones de SAP BW  
 Puede configurar el administrador de conexiones de SAP BW de las maneras siguientes:  
  
-   Facilite el cliente, el nombre de usuario, la contraseña y el idioma de la conexión.  
  
-   Elija si desea conectarse a un único servidor de aplicaciones o un grupo de servidores con equilibrio de carga.  
  
-   Proporcione el número de host y del sistema para un único servidor de aplicaciones o proporcione el servidor de mensajes, grupo y SID de un grupo de servidores con equilibrio de carga.  
  
-   Habilite el registro personalizado de llamadas a funciones RFC para los componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. (Este registro es independiente del registro opcional que puede habilitar en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]). Para habilitar el registro de las llamadas a funciones RFC, debe especificar un directorio en el que almacenar los archivos de registro que se crean antes y después de cada llamada a funciones RFC. (Esta característica de registro crea múltiples archivos de registro en formato XML. Dado que estos archivos de registro también contienen todas las filas de datos que se transfieren, es posible que los archivos de registro consuman gran cantidad de espacio en disco). Si no selecciona un directorio de registro, el registro no estará habilitado.  
  
    > [!IMPORTANT]  
    >  Si los datos que se transfieren contienen información confidencial, los archivos de registro también contendrán esa información confidencial.  
  
-   Use los valores especificados para probar la conexión.  
  
 Si no conoce todos los valores necesarios para configurar el administrador de conexiones, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 Para obtener instrucciones sobre cómo configurar y utilizar el administrador de conexiones, el origen y el destino de SAP BW, vea las notas del producto, [Usar SQL Server 2008 Integration Services con SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Estas notas del producto también muestran cómo configurar los objetos necesarios en SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Usar el Diseñador SSIS para configurar el origen  
 Para obtener más información sobre las propiedades del administrador de conexiones de SAP BW que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Editor del administrador de conexiones SAP BW](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>Vea también  
 [Componentes de Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-components.md)  
  
  
