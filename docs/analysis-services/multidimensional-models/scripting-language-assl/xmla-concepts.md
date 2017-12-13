---
title: Conceptos de XMLA | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: XMLA, concepts
ms.assetid: 816183a7-d2f7-4e14-8e5b-2a4c1798fbc1
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5dca0d0e247a985194109651ad14810d98a570e9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="xmla-concepts"></a>Conceptos de XMLA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]El estándar XML for Analysis (XMLA) abierto admite el acceso a orígenes de datos que residen en World Wide Web. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] implementa XMLA de acuerdo con la especificación XMLA 1.1.  
  
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
  
  
