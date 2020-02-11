---
title: Extensiones de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b671200dce3b5be1e01e40b09ff285563c4d4f6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62985770"
---
# <a name="reporting-services-extensions"></a>Extensiones de Reporting Services
  La arquitectura modular de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se ha diseñado para permitir ampliaciones. Hay una API de código administrado que permite desarrollar, instalar y administrar con facilidad las extensiones que usan numerosos componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Puede crear ensamblados privados o compartidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mediante y agregar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] una nueva funcionalidad para satisfacer sus necesidades empresariales en constante evolución.  
  
 La arquitectura de extensibilidad única de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] permite a los programadores extender características concretas del producto y sus componentes. Actualmente, hay numerosas funciones que permiten extender las capacidades de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La API de procesamiento de datos incluye construcciones conocidas del proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y convenciones con las que los programadores pueden integrar el procesamiento de datos adicional en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Estas extensiones de procesamiento de datos agregan funcionalidad al servidor de informes y al Diseñador de informes, lo que habilita la integración sin problemas de los datos personalizados en los informes.  
  
 Otra extensión admitida es la de entrega. La API de entrega se integra totalmente con la arquitectura de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], lo que permite usar una gran variedad de mecanismos de entrega al enviar notificaciones de informes a los usuarios. Puede extender el servidor de informes para proporcionar una entrega personalizada a los usuarios y extender las páginas de administración de suscripción del Administrador de informes para habilitar las suscripciones que usan extensiones de entrega personalizadas.  
  
 Otra extensión del servidor de informes, Extensión de personalización de definición de informe (RDCE, Report Definition Customization Extension), puede personalizar dinámicamente una definición de informe antes de pasarse al motor del procesamiento. Podría personalizar los informes según factores como los usuarios o los idiomas. Por ejemplo, podría desear implementar vistas diferentes para varios usuarios, por ejemplo, para los administradores o los miembros de un departamento, o personalizar un informe para que tuviera un diseño diferente cuando se representara en francés o en árabe.  
  
## <a name="in-this-section"></a>En esta sección  
 [Consideraciones de seguridad para las extensiones](security-considerations-for-extensions.md)  
 Describe problemas de seguridad relacionados con el desarrollo e implementación de extensiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar una extensión de procesamiento de datos](data-processing/implementing-a-data-processing-extension.md)  
 Describe los requisitos y los pasos para implementar una extensión de procesamiento de datos para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar una extensión de entrega](delivery-extension/implementing-a-delivery-extension.md)  
 Describe los requisitos y los pasos para implementar una extensión de entrega para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementar una extensión de representación](rendering-extension/implementing-a-rendering-extension.md)  
 Contiene una introducción para desarrollar extensiones de representación.  
  
 [Implementar una extensión de seguridad](security-extension/implementing-a-security-extension.md)  
 Describe los requisitos y los pasos para implementar una extensión de seguridad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Biblioteca de extensiones de Reporting Services](reporting-services-extension-library.md)  
 Contiene la referencia de programación de la biblioteca de la API de extensiones para las características de extensibilidad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
  
