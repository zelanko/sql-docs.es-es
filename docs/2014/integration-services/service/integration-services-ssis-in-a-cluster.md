---
title: Integration Services (SSIS) en un clúster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0846c7bdb0728d79dc3538eb5a46797e1b77e3db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095985"
---
# <a name="integration-services-ssis-in-a-cluster"></a>Integration Services (SSIS) en un clúster
  No se recomienda la agrupación en clústeres de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] porque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es un servicio en clúster o que reconozca clústeres, y no admite la conmutación por error de un nodo de clúster a otro. Por consiguiente, en un entorno en clúster, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se debería instalar e iniciar como un servicio independiente en cada nodo del clúster.  
  
 Aunque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es un servicio de clúster, puede configurar manualmente el servicio para que funcione como un recurso de clúster después de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] por separado en cada nodo del clúster.  
  
 Sin embargo, si la alta disponibilidad es su objetivo a la hora de establecer un entorno de hardware en clúster, puede lograr este objetivo sin configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster.  Para administrar los paquetes de cualquier nodo del clúster desde cualquier nodo del clúster, modifique el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en cada nodo del clúster. Debe modificar cada uno de estos archivos de configuración de forma que indique todas las instancias disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las que se guardan paquetes. Esta solución proporciona la alta disponibilidad que necesitan la mayoría de los clientes, sin los posibles problemas que se producen cuando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura como un recurso de clúster. Para más información sobre cómo modificar el archivo de configuración, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](integration-services-service-ssis-service.md)  
  
 Entender el rol del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es esencial para tomar una decisión informada sobre cómo configurar el servicio en un entorno en clúster. Para más información, vea [Servicio Integration Services &#40;servicio SSIS&#41;](integration-services-service-ssis-service.md).  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Descripción de los inconvenientes de configurar Integration Services como un recurso de clúster  
 A continuación se describen algunos de los posibles inconvenientes de configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster:  
  
-   Cuando se produce una conmutación por error, los paquetes en ejecución no se reinician. Puede recuperarse de los errores de paquete reiniciando los paquetes desde los puntos de comprobación. Puede reiniciar desde los puntos de comprobación sin configurar el servicio como recurso de clúster. Para obtener más información, vea [Reiniciar paquetes de usando puntos de comprobación](../packages/restart-packages-by-using-checkpoints.md).  
  
-   Al configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un grupo de recursos distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no puede utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] desde los equipos cliente para administrar los paquetes almacenados en la base de datos msdb. El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no puede delegar las credenciales en este escenario de salto doble.  
  
-   Si tiene varios grupos de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un clúster, una conmutación por error podría producir resultados inesperados. Considere el escenario siguiente. Grupo 1, que contiene el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se está ejecutando en Nodo A. Grupo 2, que también contiene el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se está ejecutando en Nodo B. Grupo 2 conmuta por error a Nodo A. El intento de iniciar otra instancia del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Nodo A produce un error porque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un servicio de instancia única. El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está intentando la conmutación por error a Nodo A también producirá un error en función de la configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Grupo 2. Si el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se había configurado para afectar a los demás servicios del grupo de recursos, se producirá un error en el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está creando la conmutación por error porque se ha producido un error en el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si el servicio se había configurado para no afectar a los demás servicios del grupo de recursos, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podrá realizar conmutación por error al Nodo A. A menos que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Grupo 2 estuviera configurado para no afectar a los demás servicios del grupo de recursos, el error del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que está conmutando por error podría hacer que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está conmutando por error también produjera un error.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener instrucciones paso a paso sobre cómo configurar el servicio Integration Services en un clúster, vea [Configurar el servicio Integration Services como recurso de clúster](../configure-the-integration-services-service-as-a-cluster-resource.md).  
  
  
