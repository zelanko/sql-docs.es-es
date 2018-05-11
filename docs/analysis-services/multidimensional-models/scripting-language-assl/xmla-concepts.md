---
title: Conceptos de XMLA | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dde41cbaeb37a1dddd090dc0197d1ad94950b401
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="xmla-concepts"></a>Conceptos de XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  El estándar abierto XML for Analysis admite el acceso a datos a orígenes de datos que residen en World Wide Web. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementa XMLA de acuerdo con la especificación XMLA 1.1.  
  
 XML for Analysis (XMLA) es un protocolo XML basado en SOAP (Protocolo simple de acceso a objetos), diseñado específicamente para el acceso universal a los datos de cualquier origen de datos multidimensionales estándar que resida en la Web. XMLA también elimina la necesidad de implementar un componente de cliente que expone el modelo de objetos componentes (COM) o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] interfaces de .NET Framework. XMLA está optimizado para Internet, donde las idas y vueltas al servidor resultan costosas en términos de tiempo y recursos, y donde las conexiones con estado a un origen de datos pueden limitar las conexiones de usuario en el servidor.  
  
 XMLA es el protocolo nativo para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], que se usa para toda interacción entre una aplicación cliente y una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] es plenamente compatible con XML for Analysis 1.1 y, además, proporciona extensiones para admitir la administración de metadatos y de sesiones e incluir capacidades de bloqueo. Tanto Objetos de administración de análisis (AMO) como ADOMD.NET utilizan el protocolo XMLA al comunicarse con una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="handling-xmla-communications"></a>Controlar las comunicaciones XMLA  
 El estándar abierto XMLA describe dos métodos generalmente accesibles: **Discover** y **Execute**. Estos métodos utilizan la arquitectura de cliente y servidor de acoplamiento flexible admitida por XML para controlar la información de entrada y de salida en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 El **Discover** método obtiene la información y los metadatos de un servicio Web. Esta información puede incluir una lista de los orígenes de datos disponibles, así como información sobre cualquiera de los proveedores de orígenes de datos. Las propiedades definen y dan forma a los datos que se obtienen de un origen de datos. El **Discover** método es un método común para definir muchos de los tipos de información que una aplicación cliente puede requerir de orígenes de datos en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancias. Las propiedades y la interfaz genérica proporcionan extensibilidad sin necesidad de volver a escribir las funciones existentes en una aplicación cliente.  
  
 El **Execute** método permite que las aplicaciones que se ejecutarán los comandos específicos del proveedor de orígenes de datos XMLA.  
  
 Aunque el protocolo XMLA está optimizado para las aplicaciones web, también se puede aprovechar para las aplicaciones orientadas a LAN. Pueden beneficiarse de esta API basada en XML las siguientes aplicaciones:  
  
-   Aplicaciones cliente/servidor que requieren una tecnología flexible entre los clientes y el servidor  
  
-   Aplicaciones cliente/servidor destinadas a diversos sistemas operativos  
  
-   Clientes que no requieren un estado relevante para aumentar la capacidad del servidor  
  
## <a name="xmla-and-the-unified-dimensional-model"></a>XMLA y el modelo UDM  
 XMLA es el protocolo que utilizan las aplicaciones de Business Intelligence que emplean la metodología del modelo UDM (Unified Dimensional Model).  
  
  
