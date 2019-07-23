---
title: Buscar GUID del conjunto de propiedades e identificadores de enteros de propiedad para las propiedades de búsqueda | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], configuring
ms.assetid: 7db79165-8bcc-4be6-8d40-12d44deda79f
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9f3784eb3a95b3da02dce2cdecc8c5db2faeaac8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082811"
---
# <a name="find-property-set-guids-and-property-integer-ids-for-search-properties"></a>Buscar GUID del conjunto de propiedades e identificadores de enteros de propiedad para las propiedades de búsqueda
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se explica cómo obtener los valores necesarios para poder agregar una propiedad a una lista de propiedades de búsqueda y hacer que se pueda buscar en ella mediante la búsqueda de texto completo. Estos valores incluyen el GUID de conjunto de propiedades y el identificador entero de propiedad de una propiedad de documento.  
  
 Las propiedades de documento que se extraen mediante IFilters de datos binarios, es decir, de datos almacenados en una columna con el tipo de datos **varbinary**, **varbinary(max)** (incluido **FILESTREAM**) o **image** pueden estar disponibles para la búsqueda de texto completo. Para que se pueda buscar una propiedad extraída, la propiedad se debe agregar manualmente una lista de propiedades de búsqueda. La lista de propiedades de búsqueda también debe estar asociada a uno o más índices de texto completo. Para obtener más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 Para poder agregar una propiedad disponible a una lista de propiedades, tiene que buscar 2 elementos de información acerca de la propiedad:  
  
-   GUID del conjunto de propiedades de la propiedad.  
  
-   Identificador entero de la propiedad.  
  
 (Cuando agrega una propiedad a una lista de propiedades, también tiene que proporcionar un nombre y una descripción. Sin embargo, no es necesario usar el nombre canónico y la descripción de la propiedad.)  
  
 En este tema se describen los métodos usados con frecuencia para buscar información sobre las propiedades disponibles, especialmente sobre las propiedades definidas por Microsoft. Para obtener información sobre las propiedades definidas por terceros, consulte la documentación de ese tercero o póngase en contacto con el proveedor.  
  
##  <a name="wellknown"></a> Buscar información acerca de las propiedades de Microsoft conocidas usadas habitualmente  
 Microsoft define centenares de propiedades de documento para su uso en muchos contextos, pero cada formato de archivo solo usa un pequeño subconjunto de las propiedades disponibles. Entre las propiedades de Windows utilizadas con frecuencia hay un pequeño conjunto de propiedades genéricas. En la tabla siguiente se muestran algunos ejemplos de propiedades genéricas conocidas. En la tabla se muestra el nombre conocido, el nombre canónico de Windows (de la descripción de propiedad publicada por Microsoft), el GUID del conjunto de propiedades, el identificador entero de la propiedad y una breve descripción.  
  
|Nombre conocido|Nombre canónico de Windows|GUID del conjunto de propiedades|Identificador entero|Descripción|  
|----------------------|----------------------------|-----------------------|----------------|-----------------|  
|Authors|**System.Author**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|4|Autor o autores de un elemento determinado.|  
|Etiquetas|**System.Keywords**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|5|Conjunto de palabras clave (también conocido como etiquetas) asignado al elemento.|  
|Tipo|**System.PerceivedType**|28636AA6-953D-11D2-B5D6-00C04FD918D0|9|Tipo de archivo percibido basado en su tipo canónico.|  
|Title|**System.Title**|F29F85E0-4FF9-1068-AB91-08002B27B3D9|2|Título del elemento. Por ejemplo, el título de un documento, el asunto de un mensaje, la leyenda de una foto o el nombre de una pista de música.|  
  
 Para fomentar la coherencia entre los formatos de archivo, Microsoft ha identificado subconjuntos de las propiedades de documento de alta prioridad usadas con frecuencia para diversas categorías de documentos. Esto incluye comunicaciones, contactos, documentos, archivos de música, imágenes y vídeos. Para obtener más información sobre las principales propiedades para cada categoría, vea la sección sobre las [propiedades definidas por el sistema para formatos de archivo personalizados](https://go.microsoft.com/fwlink/?LinkId=144336) en la documentación de Windows Search.  
  
 Un formato de archivo específico puede implementar propiedades de tres tipos:  
  
-   Propiedades genéricas definidas por [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Propiedades específicas de la categoría definidas por [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
-   Propiedades personalizadas específicas de la aplicación definidas por el proveedor de software.  
  
##  <a name="filtdump"></a> Buscar información acerca de las propiedades disponibles con FILTDUMP.EXE  
 Para saber qué propiedades detecta y extrae un IFilter instalado, puede instalar y ejecutar la utilidad **filtdump.exe** , que forma parte del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Ejecute **filtdump.exe** desde el símbolo del sistema y proporcione un único argumento. Este argumento es el nombre de un archivo individual que tiene un tipo de archivo para el que está instalado un IFilter. La utilidad muestra una lista de todas las propiedades detectadas por el IFilter en el documento, con sus GUID de conjunto de propiedades, identificadores enteros e información adicional.  
  
 Para obtener información acerca de la instalación de este software, vea [SDK de Microsoft Windows para Windows 7 y .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=212980). Después de descargar e instalar el SDK, busque en las siguientes carpetas la utilidad filtdump.exe.  
  
-   Para la versión de 64 bits, busque en `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\x64`.  
  
-   Para la versión de 32 bits, busque en `C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin`.  
  
##  <a name="propdesc"></a> Buscar valores de una propiedad de búsqueda a partir de una descripción de propiedad de Windows  
 En el caso de una propiedad de búsqueda de Windows conocida, puede obtener la información necesaria de los atributos **formatID** y **propID** de la descripción de propiedad (**propertyDescription**).  
  
 En el ejemplo siguiente se muestra la parte pertinente de una descripción de propiedad de Microsoft típica, en este caso de la propiedad `System.Author` . El atributo `formatID` especifica el GUID del conjunto de propiedades, `F29F85E0-4FF9-1068-AB91-08002B27B3D9`, y el atributo `propID` especifica el identificador entero de propiedad, `4.` Observe que el atributo `name` especifica el nombre de propiedad canónico de Windows, `System.Author`. (En este ejemplo se omiten las partes de la descripción de propiedad que no son pertinentes.)  
  
```  
.  
propertyDescription  
name = System.Author  
...  
formatID = F29F85E0-4FF9-1068-AB91-08002B27B3D9  
propID = 4  
...  
```  
  
 Para obtener la descripción completa de esta propiedad, vea [System.Author](https://go.microsoft.com/fwlink/?LinkId=144337) en la documentación de Windows Search.  
  
 Para obtener una lista completa de las propiedades de Windows, vea [Propiedades de Windows](https://go.microsoft.com/fwlink/?LinkId=215013), también en la documentación de Windows Search.  
  
##  <a name="examples"></a> Agregar una propiedad a una lista de propiedades de búsqueda  
 En el ejemplo siguiente se muestra cómo agregar una propiedad a una lista de propiedades de búsqueda. En el ejemplo se usa una instrucción [ALTER SEARCH PROPERTY LIST](../../t-sql/statements/alter-search-property-list-transact-sql.md) para agregar la propiedad `System.Author` a una lista de propiedades de búsqueda denominada `PropertyList1`y se proporciona un nombre descriptivo para la propiedad, `Author`.  
  
```  
ALTER SEARCH PROPERTY LIST PropertyList1   
  ADD 'Author'  
    WITH (  
          PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',  
          PROPERTY_INT_ID = 4,   
          PROPERTY_DESCRIPTION = 'System.Author - the author or authors of the item'   
         )  
GO  
```  
  
 Para obtener más información sobre cómo crear una lista de propiedades de búsqueda y asociarla a un índice de texto completo, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="see-also"></a>Consulte también  
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
  
