---
title: Integración de SharePoint con 2008 y 2008 R2 servidores de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d29d41069d5daca25d53477326e864720aa87ca1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101203"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>Integración de SharePoint con servidores de informes 2008 y 2008 R2
  En la versión [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se introdujo una arquitectura en la que el modo de SharePoint se basa ahora en un servicio compartido de SharePoint. Administración de la nueva funcionalidad se ha completado en Administración Central de SharePoint en el **administrar servicios** y **administrar aplicaciones de servicio** páginas. El [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] arquitectura anterior para la integración de SharePoint sigue siendo compatible con la [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint 2010 para SharePoint 2010 que pueda integrar con versiones anteriores de un servidor de informes.  
  
 Las páginas de Administración central de SharePoint que utilizaría para administrar la arquitectura anterior se encuentran en las siguientes ubicaciones:  
  
1.  Haga clic en Administración Central de SharePoint **configuración General de la aplicación**.  
  
2.  El grupo **SQL Server Reporting Services (2008 y 2008 R2)** contiene los vínculos y páginas de administración de la arquitectura anterior  
  
## <a name="server-integration-architecture"></a>Arquitectura de integración de servidor  
 Cuando se integra un servidor de informes con una instancia de un producto de SharePoint, los elementos y propiedades se almacenan en las bases de datos de contenido de SharePoint. Esto proporciona un mayor nivel de integración entre las tecnologías de servidor que afecta a la forma de almacenar, proteger y obtener acceso al contenido.  
  
 Almacenar los elementos y propiedades de un informe en las bases de datos de contenido de SharePoint permite buscar en las bibliotecas de SharePoint tipos de contenido del servidor de informes, proteger elementos con los mismos niveles de permiso y proveedor de autenticación que controla el acceso a otros documentos de la empresa hospedados en un sitio de SharePoint, usar las características de colaboración y administración de documentos para proteger y desproteger informes para su modificación, usar alertas para descubrir si se ha modificado algún elemento, e incrustar o personalizar el elemento web Visor de informes en las páginas y sitios de la aplicación. Si tiene los permisos necesarios dentro de un sitio de SharePoint, también puede generar los modelos de informe de los orígenes de datos compartidos y usar el Generador de informes para crear los informes.  
  
 El servidor de informes sigue proporcionando todas las funciones de procesamiento, representación y entrega de datos. También admite todo el procesamiento de informes programados para instantáneas e historial de informes. Cuando se abre un informe desde un sitio de SharePoint, el extremo del servidor de informes se conecta a un servidor de informes, crea una sesión, prepara el informe para que sea procesado, recupera los datos, combina el informe en el diseño de informe y lo muestra en el elemento web Visor de informes. Mientras el informe está abierto, puede exportarse a diferentes formatos de aplicación; también es posible interactuar con los datos mediante la obtención de detalles de los números subyacentes o haciendo clic hasta llegar a un informe relacionado. Las operaciones de exportación e interacción con los informes se ejecutan en el servidor de informes.  
  
 El servidor de informes sincroniza las operaciones y datos con SharePoint realiza un seguimiento de la información relativa a los archivos que procesa. Cuando se modifican las propiedades o la configuración de cualquier elemento de un servidor de informes, el cambio se almacena en una base de datos de SharePoint y después se copia en la base de datos del servidor de informes que proporciona almacenamiento interno a un servidor de informes.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Activar las características de integración del servidor de informes y Power View en SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 Describe cómo activar la característica de servidor de informes necesaria para la integración con servidores de informes de versiones anteriores.  
  
  
