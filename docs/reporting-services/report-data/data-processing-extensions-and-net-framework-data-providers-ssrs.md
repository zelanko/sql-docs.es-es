---
title: Extensiones de procesamiento de datos y proveedores de datos de .NET Framework (SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74e70cd67affe64f31076f362f36e813f3357f82
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>Extensiones de procesamiento de datos y proveedores de datos de .NET Framework (SSRS)
  Una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es un componente instalado con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], diseñado para recuperar datos de un tipo de origen de datos específico y proporcionar una funcionalidad adicional para admitir el diseño y el procesamiento de informes. Una extensión de procesamiento de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] es un componente disponible de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o de terceros que admite interfaces <xref:System.Data> que permiten recuperar y modificar datos de un tipo de origen de datos específico.  
  
## <a name="understanding-a-data-processing-extension"></a>Descripción de las extensiones de procesamiento de datos  
 Una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite un subconjunto de las interfaces de <xref:System.Data> . Las extensiones de procesamiento de datos solo requieren acceso de lectura a un origen de datos, de modo que no se implementen las interfaces para escritura y actualización. Cada extensión de procesamiento de datos puede incluir características personalizadas para admitir el procesamiento de informes. Por ejemplo, una extensión de procesamiento de datos podría admitir los tipos siguientes de características:  
  
-   Administración de credenciales independientemente de la cadena de conexión  
  
-   Admisión de parámetros de varios valores  
  
-   Recuperación de agregados de servidor, que se calculan en el origen de datos  
  
-   Recuperación de propiedades y valores de datos del origen de datos  
  
## <a name="understanding-a-data-provider"></a>Descripción de un proveedor de datos  
 Una extensión de procesamiento de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (a veces conocido como controlador) admite un conjunto estándar de las interfaces <xref:System.Data> para leer, escribir y actualizar datos en un origen de datos. Se puede usar un proveedor de datos cuando no hay ninguna extensión de procesamiento de datos disponible para un tipo específico de origen de datos. Hay disponibles diversos proveedores de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de terceros.  
  
 Debido a que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tiene una arquitectura de proveedor de datos extensible, puede generar una extensión de procesamiento de datos personalizada para incluir la funcionalidad adicional proporcionada por las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md). Para las extensiones de procesamiento de datos de terceros, vea la documentación incluida con ellas.  
  
> [!NOTE]  
>  Se debe instalar y registrar un proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] o una extensión de procesamiento de datos personalizada para poder tener acceso a los datos de un origen de datos. La extensión de procesamiento de datos se debe instalar y registrar tanto en el cliente de informes para crear el informe como en el servidor de informes para ver el informe publicado. No todos los proveedores de datos están diseñados para funcionar en un entorno de servidor. Para obtener más información, vea [Registrar un proveedor de datos estándar de .NET Framework &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md) e [Implementar una extensión de procesamiento de datos](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general de las extensiones de procesamiento de datos](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [Informe incrusta los conjuntos de datos y conjuntos de datos compartidos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  

