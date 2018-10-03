---
title: Cuadro de diálogo de propiedades (SSAS - Tabular) de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.DatabaseProperties.f1
ms.assetid: 0f0ec02f-7b55-40ea-8a04-ed0deb1efd7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f8204913babd9b52caf2edcaa2de8feae76c70d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105695"
---
# <a name="database-properties-dialog-box-ssas---tabular"></a>Cuadro de diálogo Propiedades de base de datos (SSAS: tabular)
  Este cuadro de diálogo proporciona marcas de tiempo y otra información descriptiva, además de propiedades personalizables que determinan si la base de datos usa datos almacenados en caché. Entre las propiedades personalizables se incluyen la posibilidad de cambiar el nombre de la base de datos y especificar las opciones de suplantación.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Nombre**|**Nombre** es el nombre de la base de datos que identifica exclusivamente la base de datos en el servidor. Al cambiar el nombre de la base de datos, considere el efecto en los informes y las aplicaciones cliente que utilizan el nombre actual en las cadenas de conexión existentes. Tendrá que actualizar las cadenas de conexión de los informes existentes para evitar errores de acceso denegado. Además, el modelo tabular que es el origen de esta base de datos utiliza probablemente el nombre original. Considere actualizar las propiedades de implementación del modelo para asegurarse de que las actualizaciones posteriores de ese modelo se publican en la base de datos deseada.|  
|**ID**|Muestra el identificador de la base de datos.|  
|**Descripción**|Escriba una descripción para cambiar la descripción de la base de datos.|  
|**Marca de tiempo de creación**|Muestra la fecha y hora en que se creó la base de datos.|  
|**Última actualización de esquema**|Muestra la fecha y hora en que se actualizaron por última vez los metadatos de la base de datos.|  
|**Última actualización**|Muestra la fecha y hora en que se actualizaron por última vez los datos de la base de datos.|  
|**Modo de lectura y escritura**|Es una propiedad de solo lectura, pero se puede cambiar con una secuencia de comandos **Detach** y **Attach** , donde la propiedad es un parámetro del comando **Attach** . Para más información, vea [Modos de la propiedad de base de datos ReadWriteMode](multidimensional-models/database-readwritemodes.md).|  
|**DirectQueryMode**|Especifica si la base de datos utiliza solo el almacenamiento en memoria (sin almacenamiento en disco), solo el almacenamiento basado en disco o una combinación de ambos. Los valores válidos son InMemory, DirectQuery, InMemoryWithDirectQuery (principalmente, el almacenamiento basado en memoria con cierta paginación en el disco) o DirectQueryWithInMemory (principalmente basado en disco con parte de almacenamiento en memoria). Para obtener más información, consulte [escenarios de implementación de DirectQuery &#40;Tabular de SSAS&#41;](directquery-deployment-scenarios-ssas-tabular.md).|  
|**Información de suplantación de origen de datos**|Especifica la cuenta de suplantación utilizada en las conexiones a bases de datos al procesar o actualizar los datos en las particiones locales o remotos, las consultas que se ejecutan en un almacén de datos relacional (mediante DirectQuery), los enlaces fuera de línea y la sincronización de bases de datos del destino al origen.<br /><br /> Los valores válidos incluyen la cuenta de servicio de Analysis Services o un conjunto específico de credenciales de Windows. No especifique **Usar las credenciales del usuario actual**. Esa opción de credenciales no se admite para una base de datos de modelo tabular.|  
|**Procesado por última vez**|Muestra la fecha y hora en que se procesó por última vez la base de datos.|  
|**Tamaño estimado**|Muestra el tamaño estimado de la base de datos.|  
|**Ubicación de almacenamiento**|Especifica la ubicación de la base de datos. Si la base de datos se encuentra en el directorio de datos predeterminado, este valor estará vacío.|  
  
  
