---
title: Desarrollador&#39;guía (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 067b1f69-84eb-4a13-b220-120cd63704b4
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4b204fe10d94cc875f1967aa50d8531826cd53f4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758907"
---
# <a name="developer39s-guide-master-data-services"></a>Desarrollador&#39;guía (Master Data Services)
  Obtenga información sobre cómo escribir código para personalizar la manera en que usted y sus usuarios interactúan con [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Aprenda a:  
  
-   Escribir un programa que tenga acceso al servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . El servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] es un servicio de Windows Communication Foundation (WCF) que los desarrolladores utilizan para controlar las características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] a través de código.  
  
-   Incorporar características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] en aplicaciones existentes.  
  
-   Escribir código para realizar acciones repetitivas o complejas que sean difíciles o imposibles de realizar con la interfaz de usuario de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
-   Crear un flujo de trabajo personalizado que se ejecute en respuesta a una regla de negocio que especifique. Un flujo de trabajo personalizado llama al código creado por usted, que puede realizar cualquier acción necesaria para procesar el flujo de trabajo.  
  
## <a name="master-data-manager-web-service"></a>Servicio web Master Data Manager  
 El servicio web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] le permite usar las características de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] mediante programación desde cualquier equipo que pueda acceder a su sitio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . Antes de empezar a escribir código para acceder al servicio web, debe generar clases de proxy que estén incluidas en un espacio de nombres que especifique. En esta documentación se usa <xref:Microsoft.MasterDataServices> como espacio de nombres del proxy. La clase de proxy principal que utiliza para realizar operaciones del servicio web es la clase <xref:Microsoft.MasterDataServices.ServiceClient>, que implementa la interfaz <xref:Microsoft.MasterDataServices.IService>. Desde el código, puede llamar a los métodos de la clase <xref:Microsoft.MasterDataServices.ServiceClient> para tener acceso al servicio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. El resto de las clases del espacio de nombres se utiliza en las operaciones del servicio web.  
  
### <a name="web-service-content"></a>Contenido del servicio web  
 [Crear clases de proxy del servicio web Master Data Manager](create-master-data-manager-web-service-proxy-classes.md)  
 Describe cómo se habilitan los metadatos que se publican desde el sitio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] y cómo se crean las clases de proxy que se pueden usar mediante programación para tener acceso a las operaciones del servicio web.  
  
 [Operaciones de servicio web clasificadas &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
 Lista clasificada de las operaciones de servicio web de la clase <xref:Microsoft.MasterDataServices.ServiceClient>.  
  
## <a name="custom-workflows"></a>Flujos de trabajo personalizados  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] utiliza reglas de negocio para crear soluciones básicas de flujo de trabajo. Puede actualizar y validar automáticamente los datos y enviar notificaciones por correo electrónico en función de las condiciones que especifique. Las reglas de negocio de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] están diseñadas para administrar los escenarios de flujo de trabajo más comunes. Si su flujo de trabajo requiere un procesamiento de eventos más complejos, como aprobaciones de varios niveles o árboles de decisiones complejos, puede configurar [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para que envíe datos a un ensamblado personalizado que cree. Para administrar flujos de trabajo personalizados, debe configurar e iniciar el servicio de integración de flujos de trabajo MDS de SQL Server en el equipo de la aplicación web y crear un ensamblado que implemente la interfaz <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>.  
  
### <a name="custom-workflow-content"></a>Contenido del flujo de trabajo personalizado  
 [Crear un flujo de trabajo personalizado &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)  
 Instrucciones sobre cómo crear un ensamblado que controle el flujo de trabajo, sobre cómo configurar e iniciar el servicio de integración de flujos de trabajo MDS de SQL Server y sobre cómo crear una regla de negocio en [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] que inicie un flujo de trabajo personalizado.  
  
## <a name="web-server-namespaces"></a>Espacios de nombres de servidor web  
 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] instala un conjunto de ensamblados en el equipo del servidor web. Estos ensamblados contienen espacios de nombres que se pueden usar en escenarios avanzados donde se personaliza el comportamiento del equipo del servidor web. Estos espacios de nombres se describen en la siguiente tabla.  
  
|Espacio de nombres|Descripción|  
|---------------|-----------------|  
|<xref:Microsoft.MasterDataServices.Deployment>|Contiene clases que se pueden utilizar para crear un paquete de implementación de un modelo e implementar un paquete en una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services>|Contiene una clase que recibe y procesa las operaciones del servicio web realizadas en el equipo del servidor web con la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services.DataContracts>|Contiene clases que definen cómo se pasan los datos del equipo cliente al equipo del servidor web a través de la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services.MessageContracts>|Contiene clases que definen cómo se pasan las solicitudes y respuestas del equipo cliente al equipo del servidor web a través de la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
|<xref:Microsoft.MasterDataServices.Services.ServiceContracts>|Contiene la interfaz que define las operaciones que se pueden llamar a través del servicio web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .|  
  
  
