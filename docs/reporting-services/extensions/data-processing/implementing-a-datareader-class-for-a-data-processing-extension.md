---
title: "Implementar una clase DataReader para una extensión de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
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
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: fb0f4c2f3ea3137f2e614e688aa5e3823a043e50
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>Implementar una clase DataReader para una extensión de procesamiento de datos
  El **DataReader** objeto permite que un cliente recuperar un flujo de datos de solo avance de solo lectura de un origen de datos. Resultados se devuelven cuando se ejecuta la consulta y se almacenan en el búfer de red en el cliente hasta que se solicitan con el **lectura** método de la **DataReader** clase. Para crear un **DataReader** clase, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> y, opcionalmente, implementar <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>. Con un **DataReader** objeto aumenta rendimiento de la aplicación mediante la recuperación de datos tan pronto como el está disponible, en lugar de esperar los resultados completos de la consulta se devuelve y (de forma predeterminada) almacenar solo una fila cada vez en memoria, reducir la sobrecarga del sistema.  
  
 Después de crear una instancia de la **comando** (clase), se crea un **DataReader** objeto mediante una llamada a **Command.ExecuteReader** para recuperar las filas del origen de datos. El **DataReader** implementación debe proporcionar dos capacidades básicas: acceso de solo avance sobre el resultado establece obtenido mediante la ejecución de un comando y el acceso a los tipos de columna, nombres y los valores dentro de cada fila. Los clientes utilizan la **lectura** método de la **DataReader** objeto para obtener una fila de los resultados de la consulta.  
  
 En el Diseñador de informes, el **DataReader** objeto se usa para recuperar una lista de campos, así como información de esquema sobre el conjunto de resultados. Esto se logra mediante la implementación de la **GetName**, **GetValue**, **GetFieldType,** y **GetOrdinal** métodos de la <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> interfaz.  
  
 La interfaz <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> le permite proporcionar información de agregaciones concretas acerca del conjunto de resultados. Para obtener un ejemplo **DataReader** implementación de la clase, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
