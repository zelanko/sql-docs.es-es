---
title: Administrar Service Broker
ms.custom: seo-dt-2019
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Service Broker [SMO]
ms.assetid: b29d7432-d1e5-4bb6-b544-57b3a9430f95
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3fe187412a70956d1f4496b6c042e39edafd18c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74094409"
---
# <a name="managing-service-broker"></a>Administrar Service Broker

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  En SMO, los objetos [!INCLUDE[ssSB](../../../includes/sssb-md.md)] se encuntran en el espacio de nombres **Microsoft.SqlServer.Management.Smo.Broker** , que requiere una referencia a Microsoft.SqlServer.Smo.dll. También se requiere una referencia a Microsoft.SqlServer.ServiceBrokerEnum.dll para admitir la información de clase.  
  
 SMO proporciona un conjunto de objetos [!INCLUDE[ssSB](../../../includes/sssb-md.md)] que permiten administrar mediante programación (DDL) la implementación [!INCLUDE[ssSB](../../../includes/sssb-md.md)] . Esto incluye definir los tipos de mensaje, los contratos, las colas y los servicios. Dado que SMO es una herramienta de administración que no está diseñada para la manipulación de datos, SMO no admite el envío y la recepción de mensajes de [!INCLUDE[ssSB](../../../includes/sssb-md.md)] .  
  
 En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Database.ServiceBroker%2A> es la clase de nivel superior bajo la que reside toda la funcionalidad de [!INCLUDE[ssSB](../../../includes/sssb-md.md)]. Se requiere una implementación de [!INCLUDE[ssSB](../../../includes/sssb-md.md)] para cada base de datos que participa en la aplicación de mensajería distribuida. Por consiguiente, el objeto <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> es un elemento secundario del objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceBroker> contiene colecciones de los objetos siguientes que se utilizan para definir la implementación de [!INCLUDE[ssSB](../../../includes/sssb-md.md)]:  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageType> representan tipos de mensaje que definen el contenido de los mensajes.  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.MessageTypeMapping> representan contratos que especifican la dirección y el tipo de mensajes de una conversación determinada.  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceQueue> almacenan los mensajes antes de realizar el envío y una vez recibidos. Proporcionan la comunicación asincrónica entre los servicios, así como otras ventajas, como bloquear automáticamente los mensajes del mismo grupo de conversación.  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.BrokerService> representan servicios de [!INCLUDE[ssSB](../../../includes/sssb-md.md)], que son extremos direccionables para las conversaciones. Los mensajes de [!INCLUDE[ssSB](../../../includes/sssb-md.md)] se envían desde un servicio hasta otro. Un servicio especifica una cola para retener mensajes y los contratos en los que el servicio puede ser el destino.  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.RemoteServiceBinding> representan los valores que [!INCLUDE[ssSB](../../../includes/sssb-md.md)] utiliza para la seguridad y autenticación al comunicar con un servicio remoto.  
  
-   Los objetos <xref:Microsoft.SqlServer.Management.Smo.Broker.ServiceRoute> representan una ruta de [!INCLUDE[ssSB](../../../includes/sssb-md.md)], que contiene la información de ubicación para el servicio y la base de datos en las que se define. Se requiere una ruta para la entrega del mensaje. De forma predeterminada, cada base de datos contiene una ruta que especifica la ubicación como la instancia actual de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>   
 [SQL Server Service Broker](../../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
