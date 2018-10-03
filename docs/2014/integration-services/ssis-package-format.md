---
title: Formato de paquetes de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 43c0662c9084c654b4138a8443f1e2e98eaec376
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200025"
---
# <a name="ssis-package-format"></a>Formato de paquetes SSIS
  En la versión actual de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], se han realizado cambios significativos en el formato de paquetes (archivo .dtsx) para que sea más fácil leer el formato y comparar paquetes. También puede combinar de forma más confiable paquetes que no contienen cambios en conflicto o cambios almacenados en formato binario.  
  
 Para ver el formato de archivo del paquete actual DTSX, vea [\[MS-DTSX\]: Data Transformation Services Package XML File Format Specification ([MS-DTSX]: Especificación del formato de archivo XML de paquete de servicios de transformación de datos)](http://go.microsoft.com/fwlink/?LinkId=233251).  
  
 En la lista siguiente se mencionan los cambios de formato de archivo. Para ver ejemplos de código de estos cambios, vea [Cambios de formato de paquetes en SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=233255)  
  
-   Las convenciones de formato se han aplicado para que sea más fácil leer y comprender el archivo .dtsx.  
  
-   El formato es más conciso. Los elementos independientes de cada propiedad se han guardado como atributos, excepto PackageFormatVersion. Los atributos se muestran en orden alfabético y las propiedades que tienen valores predeterminados ya no se guardan. Finalmente, los elementos que pueden aparecer varias veces, ahora se encuentran dentro de un elemento primario.  
  
-   La mayoría de los objetos dentro de un paquete al que se puede hacer referencia mediante otros objetos ahora tienen un atributo `refId` definido en el paquete XML. En lugar los identificadores de linaje de almacenamiento, ahora se guarda `refID`. Los identificadores de linaje todavía se utilizan en tiempo de ejecución y se vuelven a generar al cargar el paquete.  
  
     El `refId` valor es una cadena única que es legible y fácil comprensión, comparará con GUID o valores enteros. La cadena es similar a los valores de ruta de acceso que se usan para las configuraciones de paquetes en versiones anteriores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Si va a combinar los cambios entre las dos versiones de un paquete, el `refId` puede utilizarse en operaciones de búsqueda y reemplazo para asegurarse de que todas las referencias a ese objeto se han actualizado correctamente.  
  
-   La información de diseño se encuentra en una sección de CDATA.  
  
-   Las anotaciones se conservan en texto no cifrado. Esto hace más fácil extraer la información para la generación automatizada de documentación.  
  
  
