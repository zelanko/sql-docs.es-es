---
title: Conectarse a Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7b0e2b4020f3f9d27be84c1a6dc2f0944da88f5f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="connect-to-analysis-services"></a>Conectar a Analysis Services
  Utilice la información de esta sección para obtener datos acerca de las propiedades de la cadena de conexión, las bibliotecas de cliente usadas para las conexiones, los métodos de autenticación que admite Analysis Services y cómo configurar o desactivar conexiones antes de desconectar un servidor.  
  
## <a name="analysis-services-connections"></a>Conexiones de Analysis Services  
 Analysis Services usa TCP como protocolo de red y XML for Analysis (XMLA) como protocolo de comunicación. En el nivel inferior, todas las bibliotecas de cliente incluidas en Analysis Services que implementan XMLA sobre TCP. Si bien es posible compilar aplicaciones basadas en XMLA sin formato, la mayoría de las aplicaciones y los desarrolladores de aplicaciones emplean bibliotecas de cliente para aprovechar los modelos de objetos y las eficiencias de código que proporcionan. Para conexiones de cliente a Analysis Services se puede utilizar IIS como conexión intermediaria si no se puede utilizar TCP a través de la pila. Una ventaja de utilizar el acceso HTTP a través de IIS es la capacidad de conectarse desde aplicaciones que pasan las credenciales en la cadena de conexión.  
  
 Cualquier descripción que hable de la conectividad suele incluir la autenticación. A diferencia de otras características de SQL Server, Analysis Services utiliza exclusivamente las credenciales de Windows. En la conexión de back-end de Analysis Services no se puede usar autenticación de base de datos de SQL Server, autenticación de notificaciones, autenticación basada en formularios o autenticación implícita. En esta sección se ofrece más información acerca de la autenticación.  
  
##  <a name="bkmk_clientApps"></a> Tareas de conexión  
  
|Vínculo|Descripción de la tarea|  
|----------|----------------------|  
|[Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|Si no está familiarizado con Analysis Services, lea este tema para conocer las herramientas y las aplicaciones de uso más frecuente con Analysis Services.|  
|[Propiedades de cadena de conexión &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services incluye numerosas propiedades de servidor y base de datos, lo que permite personalizar una conexión para una aplicación específica, independientemente de cómo esté configurada la instancia o la base de datos.|  
|[Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|Este tema es una breve introducción a los métodos de autenticación que Analysis Services usa.|  
|[Configurar Analysis Services para la delegación restringida de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|Muchas soluciones de Business Intelligence necesitan suplantación para asegurarse de que solo se devuelven los datos autorizados a cada usuario. En este tema, aprenderá los requisitos para usar la suplantación. En este tema también se explican los pasos para configurar Analysis Services para la delegación limitada de Kerberos.|  
|[Registro de SPN para una instancia de Analysis Services](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|La autenticación Kerberos necesita un nombre principal del servicio (SPN) válido para los servicios que suplantan o delegan identidades de usuario en soluciones multiservidor. Use la información de este tema para conocer la construcción y los pasos para el registro de SPN para Analysis Services.|  
|[Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|La autenticación básica o los límites entre dominios son dos motivos importantes para configurar Analysis Services para el acceso HTTP.|  
|[Proveedores de datos usados para conexiones de Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services proporciona tres bibliotecas de cliente para el acceso a operaciones de servidor o a datos de Analysis Services. Este tema proporciona una breve introducción a ADOMD.NET, Objetos de administración de Analysis Services (AMO) y el proveedor OLE DB de Analysis Services (MSOLAP).|  
|[Desconectar usuarios y sesiones en el servidor de Analysis Services](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|Desactive las conexiones y sesiones existentes antes de poner un servidor sin conexión o de realizar pruebas de rendimiento de línea base.|  
  
## <a name="see-also"></a>Vea también  
 [Configuración posterior a la instalación &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Propiedades del servidor de Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  

