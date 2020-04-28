---
title: Servicios de datos de referencia en DQS
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 6d3c4f15dcb62e36918c81baa5f2bd40c38b7c6a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75244136"
---
# <a name="reference-data-services-in-dqs"></a>Servicios de datos de referencia en DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Los datos de referencia hacen referencia a un conjunto completo y preciso de datos globales relacionados o clasificados (más allá de los límites de una empresa) que está disponible en dominios públicos de confianza o en proveedores de contenido comercial premium.  
  
 La característica Reference Data Service de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) le permite suscribirse a proveedores de datos de referencia de terceros, y limpiar y enriquecer fácilmente sus datos empresariales validándolos con los datos de alta calidad de dichos proveedores. Puede utilizar servicios de proveedores de servicios de calidad de datos punteros desde DQS para normalizar, corregir o enriquecer los datos durante el proceso de limpieza. Por ejemplo, puede comparar una lista de prefijos telefónicos o de códigos postales con los datos de referencia para validar las direcciones de sus clientes.  
  
 La característica Reference Data Service ofrece las ventajas siguientes:  
  
-   Los datos de referencia le permiten garantizar la calidad de los datos comparándoles con los datos garantizados por una empresa de terceros.  
  
-   El proceso de datos de referencia se incorpora en la generación de bases de conocimiento de DQS y en los proyectos de calidad de datos, lo que le permite establecer un proceso de calidad de datos completo.  
  
-   Admite el uso de datos de referencia de Azure Marketplace, así como directamente de proveedores de datos de referencia de terceros.  
  
##  <a name="using-reference-data-from-azure-marketplace"></a><a name="Marketplace"></a>Uso de datos de referencia de Azure Marketplace  
 DQS admite el uso de datos de referencia de Azure Marketplace para permitir a los proveedores de contenido proporcionar servicios de datos de referencia a través de Marketplace. Marketplace es un servicio de Microsoft que proporciona un único canal de catálogo de soluciones y entrega de datos de alta calidad y aplicaciones como servicio basado en nube. Para obtener más información acerca de Marketplace, consulte más informaciónhttps://azuremarketplace.microsoft.com/about) [sobre Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/about) (.
  
 La perfecta integración entre Marketplace y DQS simplifica los pasos asociados con la detección, búsqueda y adquisición de información para los proyectos de calidad de datos desde DQS. Los datos se utilizan desde DQS, y los usuarios de DQS pueden conseguir datos de alta calidad aunando las características de DQS, Marketplace y los proveedores de servicios de datos de referencia de una manera innovadora.  
  
 Para utilizar los datos de referencia de Marketplace en DQS para la actividad de limpieza, es necesario disponer de una clave de cuenta de Marketplace. La creación de una clave de cuenta de Marketplace es gratuita, y solo deberá pagar si se suscribe a conjuntos de datos de pago. La suscripción a conjuntos de datos gratuitos, así como su uso, no supone ningún cargo. Para obtener información detallada sobre cómo crear una clave de cuenta de Marketplace, veahttps://go.microsoft.com/fwlink/?LinkId=212936) [crear su cuenta](https://go.microsoft.com/fwlink/?LinkId=212936) (.  
  
 Además, puede realizar las siguientes actividades de Marketplace desde DQS:  
  
-   Examinar conjuntos de datos en Marketplace.  
  
-   Crear una clave de cuenta de Marketplace.  
  
-   Administrar los detalles de la cuenta de Marketplace, como las claves de cuenta y las suscripciones a los proveedores de datos.  
  
 Puede realizar estas actividades en la pestaña **Datos de referencia** de la pantalla **Configuración** de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
##  <a name="using-reference-data-directly-from-the-third-party-reference-data-providers"></a><a name="Direct"></a> Usar datos de referencia directamente de los proveedores de datos de referencia de terceros  
 Si no está conectado a Internet y no puede usar Marketplace, DQS también admite la conexión directa con los proveedores de datos que estén disponibles en la red de la organización. Si desea utilizar datos de referencia de un proveedor directo de datos de referencia de terceros en línea, deberá crear un registro para dicho proveedor en DQS.  
  
##  <a name="how-to-cleanse-data-by-using-the-reference-data"></a><a name="HowToCleanse"></a> Cómo limpiar datos mediante el uso de datos de referencia  
 La limpieza de los datos en DQS mediante los datos de referencia incluye los tres pasos siguientes:  
  
1.  **Configurar los detalles del proveedor de datos de referencia en DQS**: si desea usar datos de referencia en DQS, deberá configurar en este los detalles del servicio de datos de referencia.  
  
    1.  Si usa Marketplace, proporcione una clave de cuenta de Marketplace válida, busque la categoría de datos [Data Services](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=data-services) en Marketplace y suscríbase a los proveedores necesarios.  
  
    2.  Si utiliza un proveedor directo de datos de referencia de terceros en línea, deberá agregar los detalles de este a DQS para poder utilizarlo.  
  
     La configuración de los detalles del proveedor de datos de referencia en DQS es una actividad que se realiza una sola vez para cada proveedor de datos. Solo los administradores de DQS pueden configurar los valores de los datos de referencia en DQS.  
  
2.  **Asignar un dominio o un dominio compuesto de una base de conocimiento al servicio de datos de referencia**: asigne un dominio o un dominio compuesto al servicio de datos de referencia apropiado suscrito/agregado en el paso 1.  
  
3.  **Utilizar los dominios asignados para la actividad de limpieza en un proyecto de calidad de datos**: al crear un proyecto de calidad de datos para la actividad **Limpieza** , seleccione la base de conocimiento que contiene los dominios o dominios compuestos asignados a los servicios de datos de referencia en el paso 2 y realice la actividad de limpieza.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo configurar DQS para utilizar los servicios de datos de referencia de Marketplace o de proveedores directos de datos de terceros en línea.|[Configurar DQS para utilizar datos de referencia](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Describe cómo asignar un dominio o un dominio compuesto de una base de conocimiento a un servicio de datos de referencia.|[Adjuntar un dominio o un dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Describe cómo limpiar los datos mediante el servicio de datos de referencia.|[Limpiar datos mediante el conocimiento de datos de referencia &#40;externo&#41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
