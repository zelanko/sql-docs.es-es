---
title: "Información general de las extensiones de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], about extensions
ms.assetid: 1d652605-9313-4c75-98b4-ba4dcbbb222d
caps.latest.revision: 39
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c30ea734a30e00fdefeb9b30a1ced9c3f60d5fca
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="data-processing-extensions-overview"></a>Introducción a las extensiones de procesamiento de datos
  Las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permiten conectarse a los orígenes de datos y recuperar los datos. También actúan como puente entre un origen de datos y un conjunto de datos. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]las extensiones de procesamiento de datos se modelan con un subconjunto de la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] interfaces del proveedor de datos.  
  
 En la tabla siguiente se enumeran las extensiones de procesamiento de datos incluidas con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Extensión de procesamiento de datos|Description|  
|-------------------------------|-----------------|  
|Extensión de procesamiento de datos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Usa el proveedor de datos de .NET Framework para SQL Server para conectarse y recuperar datos de la [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)].|  
|Extensión de procesamiento de datos para OLE DB|Usa el proveedor de datos de .NET Framework para OLE DB. Con esta extensión, el servidor de informes puede consultar cualquier origen de datos que tenga un proveedor OLE DB.|  
|Extensión de procesamiento de datos para Oracle|Utiliza el proveedor de datos de .NET Framework para Oracle. Con esta extensión, el servidor de informes puede tener acceso a los orígenes de datos de Oracle a través del software de conectividad de cliente de Oracle.|  
|Extensión de procesamiento de datos para ODBC|Usa el proveedor de datos de .NET Framework para ODBC. Con esta extensión, el servidor de informes puede tener acceso a los datos de cualquier base de datos para la que haya un controlador ODBC.|  
  
 Puede utilizar la API de procesamiento de datos de [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] para agregar un procesamiento de datos personalizado al servidor de informes.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] tiene compatibilidad integrada con los proveedores de datos en [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Si ya ha implementado un proveedor de datos completo, no necesita implementar una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Sin embargo, debería considerar extender el proveedor de datos para que incluya la funcionalidad concreta para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 2005, que incluye las credenciales de conexión seguras y los agregados del lado servidor.  
  
 Cada una de las extensiones de procesamiento de datos incluidas con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa un conjunto común de interfaces. De esta forma se asegura de que cada extensión implementa una funcionalidad comparable.  
  
 Puede desarrollar extensiones de procesamiento de datos para sus propios orígenes de datos o puede utilizar las interfaces con el fin de agregar un nivel adicional de procesamiento de datos a las infraestructuras de base de datos comunes. Puede implementar extensiones de procesamiento de datos personalizadas para habilitar la integración sin problemas de los datos en los servidores de informes existentes en una organización. También puede utilizarlas como parte de un conjunto de informes de errores personalizado que se proporciona a los consumidores.  
  
 ![Arquitectura de extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/media/bk-dataprocess-extensions.gif "Data processing extension architecture")  
Arquitectura de extensión de procesamiento de datos de Reporting Services  
  
 Entre las ventajas de implementar una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] personalizada se incluyen las siguientes:  
  
-   Una arquitectura de acceso a datos simplificada, a menudo con un mejor mantenimiento y rendimiento.  
  
-   La capacidad de exponer directamente la funcionalidad específica de la extensión a los consumidores.  
  
-   Una interfaz concreta para los consumidores que permite tener acceso al origen de datos dentro de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
## <a name="data-extension-process-flow"></a>Flujo del proceso de la extensión de datos  
 Antes de desarrollar la extensión de datos personalizada, debería entender cómo usa el servidor de informes las extensiones de datos para procesar los datos. También debería saber los constructores y los métodos a los que el servidor de informes llama.  
  
 ![Flujo del proceso de extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/media/bk-ext-01.gif "Process flow for data processing extension")  
El flujo del proceso paso a paso de una extensión de datos a la que el servidor de informes llama  
  
 En esta ilustración se muestra el siguiente flujo de eventos:  
  
1.  El servidor de informes crea un objeto de conexión y lo pasa en la cadena de conexión y en las credenciales asociadas al informe.  
  
2.  El texto de comando del informe se utiliza para crear un objeto de comando. En el proceso, la extensión de procesamiento de datos puede incluir código que analiza el texto del comando y crea los parámetros para el comando.  
  
3.  Una vez procesados el objeto de comando y cualquier parámetro, se genera un lector de datos que devuelve un conjunto de resultados y permite al servidor de informes asociar los datos del informe al diseño del informe.  
  
## <a name="developer-requirements"></a>Requisitos para el programador  
 Al desarrollar una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], es necesario tener lo siguiente:  
  
-   Un equipo de implementación con el Diseñador de informes o un servidor de informes instalado.  
  
-   Un equipo de desarrollo con [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] o superior, o la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Kit de desarrollo de Software (SDK) instalado.  
  
-   Una comprensión detallada de las características y capacidades de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   Una comprensión detallada de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] arquitectura, [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proveedores de datos, objetos DataSet de ADO.NET y common [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] interfaces.  
  
-   Experiencia de desarrollo de un [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] lenguaje como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] . NET.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
