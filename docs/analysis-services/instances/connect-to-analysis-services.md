---
title: Conectarse a Analysis Services | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84a37af402d691ee7507fe923a6ae765b622631f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="connect-to-analysis-services"></a>Conectar a Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Utilice la información de esta sección para obtener datos acerca de las propiedades de la cadena de conexión, las bibliotecas de cliente usadas para las conexiones, los métodos de autenticación que admite Analysis Services y cómo configurar o desactivar conexiones antes de desconectar un servidor.  

Para obtener información sobre cómo conectarse a Analysis Services de Azure, vea [conectarse a un servidor](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect).
  
## <a name="analysis-services-connections"></a>Conexiones de Analysis Services  
 Analysis Services usa TCP como protocolo de red y XML for Analysis (XMLA) como protocolo de comunicación. En el nivel inferior, todas las bibliotecas de cliente incluidas en Analysis Services que implementan XMLA sobre TCP. Si bien es posible compilar aplicaciones basadas en XMLA sin formato, la mayoría de las aplicaciones y los desarrolladores de aplicaciones emplean bibliotecas de cliente para aprovechar los modelos de objetos y las eficiencias de código que proporcionan. Para conexiones de cliente a Analysis Services se puede utilizar IIS como conexión intermediaria si no se puede utilizar TCP a través de la pila. Una ventaja de utilizar el acceso HTTP a través de IIS es la capacidad de conectarse desde aplicaciones que pasan las credenciales en la cadena de conexión.  
  
 Cualquier descripción que hable de la conectividad suele incluir la autenticación. A diferencia de otras características de SQL Server, Analysis Services utiliza exclusivamente las credenciales de Windows. En la conexión de back-end de Analysis Services no se puede usar autenticación de base de datos de SQL Server, autenticación de notificaciones, autenticación basada en formularios o autenticación implícita. En esta sección se ofrece más información acerca de la autenticación.  
  
##  <a name="bkmk_clientApps"></a> Tareas de conexión  
  
|Vínculo|Descripción de la tarea|  
|----------|----------------------|  
|[Conectarse desde aplicaciones cliente & #40; Analysis Services & #41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)|Si no está familiarizado con Analysis Services, lea este tema para conocer las herramientas y las aplicaciones de uso más frecuente con Analysis Services.|  
|[Propiedades de la cadena de conexión & #40; Analysis Services & #41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)|Analysis Services incluye numerosas propiedades de servidor y base de datos, lo que permite personalizar una conexión para una aplicación específica, independientemente de cómo esté configurada la instancia o la base de datos.|  
|[Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)|Este tema es una breve introducción a los métodos de autenticación que Analysis Services usa.|  
|[Configurar Analysis Services para delegación limitada de Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)|Muchas soluciones de Business Intelligence necesitan suplantación para asegurarse de que solo se devuelven los datos autorizados a cada usuario. En este tema, aprenderá los requisitos para usar la suplantación. En este tema también se explican los pasos para configurar Analysis Services para la delegación limitada de Kerberos.|  
|[Registro de SPN para una instancia de Analysis Services](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)|La autenticación Kerberos necesita un nombre principal del servicio (SPN) válido para los servicios que suplantan o delegan identidades de usuario en soluciones multiservidor. Use la información de este tema para conocer la construcción y los pasos para el registro de SPN para Analysis Services.|  
|[Configurar el acceso HTTP a Analysis Services de servicios de Internet Information Server & #40; IIS & #41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|La autenticación básica o los límites entre dominios son dos motivos importantes para configurar Analysis Services para el acceso HTTP.|  
|[Proveedores de datos utilizados para las conexiones de Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)|Analysis Services proporciona tres bibliotecas de cliente para el acceso a operaciones de servidor o a datos de Analysis Services. Este tema proporciona una breve introducción a ADOMD.NET, Objetos de administración de Analysis Services (AMO) y el proveedor OLE DB de Analysis Services (MSOLAP).|  
|[Desconectar usuarios y sesiones en el servidor de Analysis Services](../../analysis-services/instances/disconnect-users-and-sessions-on-analysis-services-server.md)|Desactive las conexiones y sesiones existentes antes de poner un servidor sin conexión o de realizar pruebas de rendimiento de línea base.|  
  
## <a name="see-also"></a>Vea también  
 [Configuración posterior a la instalación & #40; Analysis Services & #41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)   
 [Propiedades del servidor de Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
  
  
