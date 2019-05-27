---
title: Formato de paquetes de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f59ed0eee86f17fdda568caa5c1a1dc7252c6d9c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055350"
---
# <a name="ssis-package-format"></a>Formato de paquetes SSIS
  En la versión actual de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], se han realizado cambios significativos en el formato de paquetes (archivo .dtsx) para que sea más fácil leer el formato y comparar paquetes. También puede combinar de forma más confiable paquetes que no contienen los cambios en conflicto o cambios almacenados en formato binario.  
  
 Para ver el formato de archivo de paquete actual DTSX, vea [ \[MS-DTSX\]: Especificación de formato de archivo XML de paquete de servicios de transformación de datos](https://go.microsoft.com/fwlink/?LinkId=233251).  
  
 En la lista siguiente se mencionan los cambios de formato de archivo. Para ver ejemplos de código de estos cambios, vea [Cambios de formato de paquetes en SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=233255)  
  
-   Las convenciones de formato se han aplicado para que sea más fácil leer y comprender el archivo .dtsx.  
  
-   El formato es más conciso. Los elementos independientes de cada propiedad se han guardado como atributos, excepto PackageFormatVersion. Los atributos se muestran en orden alfabético y las propiedades que tienen valores predeterminados ya no se guardan. Finalmente, los elementos que pueden aparecer varias veces, ahora se encuentran dentro de un elemento primario.  
  
-   La mayoría de los objetos dentro de un paquete al que se puede hacer referencia mediante otros objetos ahora tienen un atributo `refId` definido en el paquete XML. En lugar los identificadores de linaje de almacenamiento, ahora se guarda `refID`. Los identificadores de linaje todavía se utilizan en tiempo de ejecución y se vuelven a generar al cargar el paquete.  
  
     El valor de `refId` es una cadena única que es legible y de fácil comprensión, comparará con GUID o los valores enteros. La cadena es similar a los valores de ruta de acceso que se usan para las configuraciones de paquetes en versiones anteriores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Si se mezclan los cambios entre dos versiones de un paquete, `refId` se puede utilizar en operaciones de búsqueda y reemplazo para asegurarse de que todas las referencias al objeto se han actualizado correctamente.  
  
-   La información de diseño se encuentra en una sección de CDATA.  
  
-   Las anotaciones se conservan en texto no cifrado. Esto hace más fácil extraer la información para la generación automatizada de documentación.  
  
  
