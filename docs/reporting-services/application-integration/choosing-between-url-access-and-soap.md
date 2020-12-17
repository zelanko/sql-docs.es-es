---
title: Elección entre el acceso URL y SOAP
description: 'Hay dos maneras de integrar Reporting Services en las aplicaciones personalizadas: el acceso URL y la API de SOAP de Reporting Services. Descubra cómo elegir.'
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.custom: seo-lt-2019
ms.topic: reference
author: maggiesMSFT
ms.author: maggies
monikerRange: = sql-server-2016
ms.openlocfilehash: bab3605274c3858577fa1bb5f82743c6cd447772
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484367"
---
# <a name="choose-between-url-access-and-soap-in-reporting-services"></a>Elección entre acceso URL y SOAP en Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en aplicaciones personalizadas puede resultar complicado. El reto, sin embargo, no es la complejidad del modelo de programación o API, sino las muchas maneras posibles de integrarlo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se diseñó desde el principio como una plataforma para programadores y, como tal, se ha creado teniendo en mente la flexibilidad de la programación. Con la flexibilidad viene la necesidad de tomar decisiones importantes sobre cómo integrar la funcionalidad de la administración y navegación en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales existentes.

> [!NOTE]
> A partir de SQL Server 2017 Reporting Services, el acceso de API de REST está disponible para el desarrollo de soluciones. El acceso de API de SOAP está en desuso. Para más información, vea [Desarrollar con las API de REST para Reporting Services](../developer/rest-api.md).
  
 Hay dos maneras de integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en aplicaciones personalizadas: el acceso URL y la API de SOAP de Reporting Services. Cuál usar depende de varios factores. En algunos casos, la integración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en las aplicaciones empresariales personalizadas exige el uso de acceso URL y SOAP. Debería formular las preguntas siguientes:  
  
-   ¿Qué tipo de funcionalidad de informes empresariales requieren usted o sus usuarios finales? ¿Necesita una manera simple de iniciar y navegar por los informes, o más características avanzadas de administración de servidores de informes con la solución empresarial personalizada?  
  
-   ¿En qué tipo de entorno trabajan los usuarios normalmente? ¿La aplicación empresarial está destinada a la Web o a Windows? ¿Les resulta fácil a los usuarios finales pasar de un entorno Win32 a un entorno web? ¿Qué tipo de control necesita sobre el entorno y qué informes se ejecutan y administran?  
  
 Cuando haya respondido las preguntas anteriores, podrá decidir cómo integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la infraestructura de IT. Normalmente, el acceso URL es más adecuado para ver informes individuales y navegar por ellos. El acceso URL permite navegar libre y rápidamente por los informes sin la sobrecarga del servicio web. Asimismo, el acceso URL es, en este momento, la única técnica de programación que utiliza el Visor HTML completo para la navegación por el informe, incluida su barra de herramientas. Además, el acceso URL proporciona mejor rendimiento que SOAP porque omite el cálculo de referencias de las solicitudes SOAP que proceden del servidor o se dirigen a él. En escenarios de integración que requieren un acceso rápido y fácil a los informes con herramientas integradas para la visualización y navegación, el acceso URL es la mejor opción.  
  
> [!NOTE]  
> El acceso URL del servidor de informes admite el Visor HTML y la funcionalidad extendida de la barra de herramientas del informe. La API SOAP no admite este tipo de informe representado. Si representa informes mediante la API de SOAP, diseñe y desarrolle su propia barra de herramientas de informes.
  
 Para más información sobre la barra de herramientas de informes, vea [Visor HTML y la barra de herramientas del informe](../../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
 Para más información sobre el acceso URL, vea [Acceso URL](../../reporting-services/url-access-ssrs.md).  
  
 El acceso URL es útil para ver los informes, pero no proporciona la funcionalidad de administración de espacios de nombres e informes que puede ser esencial para cualquier escenario con informes empresariales. En este caso, se recomienda la variada y completa funcionalidad de la API SOAP de Reporting Services. Con la API SOAP, puede administrar e implementar informes, crear calendarios, configurar las propiedades del servidor, administrar el espacio de nombres del servidor de informes, crear suscripciones, etcétera. La API SOAP expone el conjunto completo de funcionalidad de administración en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La API SOAP también puede habilitar la visualización y navegación en los informes a través del método <xref:ReportExecution2005.ReportExecutionService.Render%2A> de la API. Pero al ver los informes a través de la API de SOAP, no se habilita la funcionalidad de vista integrada de la barra de herramientas de informes, ni se administra automáticamente la interactividad de los informes que proporciona el acceso URL.  
  
 Para más información sobre la API de SOAP de Reporting Services, vea [Servicio web del servidor de informes](../../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 En la mayoría de los casos, para satisfacer las necesidades de funcionalidad de informe se requieren tanto el acceso URL como las llamadas a SOAP. SOAP se usa al conectarse inicialmente a la base de datos del servidor de informes y presentar la lista disponible de informes en una interfaz de usuario, mientras que el acceso URL se utiliza para obtener realmente acceso y navegar por informes individuales.  
  
 Para obtener un ejemplo de cómo combinar el acceso URL y el servicio web para proporcionar informes integrados, vea [SQL Server Reporting Services Product Samples (Ejemplos del producto SQL Server Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=177889).

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
