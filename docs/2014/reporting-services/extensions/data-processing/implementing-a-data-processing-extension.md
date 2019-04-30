---
title: Implementar una extensión de procesamiento de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2efc74fa2ba84335fcb5e03b42125fb9c6782f43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164111"
---
# <a name="implementing-a-data-processing-extension"></a>Implementar una extensión de procesamiento de datos
  Las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permiten conectarse a los orígenes de datos y recuperar los datos. También actúan como puente entre un origen de datos y un conjunto de datos. Las extensiones de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se modelan según un subconjunto de las interfaces del proveedor de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Introducción a las extensiones de procesamiento de datos](data-processing-extensions-overview.md)  
 Explica cómo escribir una extensión de procesamiento de datos personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparación de la implementación de una extensión de procesamiento de datos](preparing-to-implement-a-data-processing-extension.md)  
 Describe las interfaces disponibles al implementar una extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], así como cuando tiene que implementar una interfaz determinada.  
  
 [Creación de una biblioteca de extensión de procesamiento de datos](creating-a-data-processing-extension-library.md)  
 Describe cómo asignar un espacio de nombres para la extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y compilar la extensión de procesamiento de datos en una DLL de biblioteca.  
  
 [Implementación de una clase Connection para una extensión de procesamiento de datos](implementing-a-connection-class-for-a-data-processing-extension.md)  
 Describe los atributos de una conexión y cómo implementar una clase propia **Connection** para la extensión de procesamiento de datos.  
  
 [Implementación de una clase Command para una extensión de procesamiento de datos](implementing-a-command-class-for-a-data-processing-extension.md)  
 Describe los atributos de un comando y cómo implementar una clase propia **Command** para la extensión de procesamiento de datos.  
  
 [Implementación de una clase DataReader para una extensión de procesamiento de datos](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Describe los atributos de un lector de datos y cómo implementar una clase propia **DataReader** para la extensión de procesamiento de datos.  
  
 [Uso de un conjunto de datos externo con Reporting Services](using-an-external-dataset-with-reporting-services.md)  
 Describe cómo exponer los objetos **DataSet** personalizados en el servidor de informes para su uso.  
  
 [Implementación de una extensión de procesamiento de datos](deploying-a-data-processing-extension.md)  
 Describe cómo implementar la extensión de procesamiento de datos.  
  
 [Depuración del código de extensión de procesamiento de datos](debugging-data-processing-extension-code.md)  
 Describe cómo depurar el código de las extensiones de procesamiento de datos.  
  
 [Eliminación de una extensión de procesamiento de datos](removing-a-data-processing-extension.md)  
 Describe cómo quitar una extensión de procesamiento de datos de un servidor de informes o del Diseñador de informes.  
  
 Para obtener un ejemplo de una extensión de procesamiento de datos totalmente implementada, vea [Ejemplos del producto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
