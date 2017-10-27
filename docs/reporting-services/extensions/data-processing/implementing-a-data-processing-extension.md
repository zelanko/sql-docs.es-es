---
title: "Implementar una extensión de procesamiento de datos | Documentos de Microsoft"
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
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 1497690ebccc010601542308747240d0e91d89db
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-data-processing-extension"></a>Implementar una extensión de procesamiento de datos
  Las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permiten conectarse a los orígenes de datos y recuperar los datos. También actúan como puente entre un origen de datos y un conjunto de datos. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]las extensiones de procesamiento de datos se modelan con un subconjunto de la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] interfaces del proveedor de datos.  
  
## <a name="in-this-section"></a>En esta sección  
 [Información general de las extensiones de procesamiento de datos](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 Explica cómo escribir una extensión de procesamiento de datos personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparación para implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 Describe las interfaces disponibles al implementar una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], así como cuando tiene que implementar una interfaz determinada.  
  
 [Crear una biblioteca de extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 Describe cómo asignar un espacio de nombres para la extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y compilar la extensión de procesamiento de datos en una DLL de biblioteca.  
  
 [Implementar una clase de conexión para una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 Describe los atributos de una conexión y cómo implementar su propia **conexión** clase para la extensión de procesamiento de datos.  
  
 [Implementar una clase de comando para una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 Describe los atributos de un comando y cómo implementar su propia **comando** clase para la extensión de procesamiento de datos.  
  
 [Implementar una clase DataReader para una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Describe los atributos de un lector de datos y cómo implementar su propia **DataReader** clase para la extensión de procesamiento de datos.  
  
 [Con un conjunto de datos externo con Reporting Services](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 Describe cómo exponer su personalizado **conjunto de datos** objetos en el servidor de informes para su uso.  
  
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 Describe cómo implementar la extensión de procesamiento de datos.  
  
 [Depuración de código de la extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 Describe cómo depurar el código de las extensiones de procesamiento de datos.  
  
 [Quitar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 Describe cómo quitar una extensión de procesamiento de datos de un servidor de informes o del Diseñador de informes.  
  
 Para obtener un ejemplo de una extensión de procesamiento de datos implementada totalmente, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

