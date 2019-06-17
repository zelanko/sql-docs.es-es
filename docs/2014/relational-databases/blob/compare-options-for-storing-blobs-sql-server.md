---
title: Comparar opciones para almacenar objetos Blob (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d682257669753665ac397133fcdec0f52e46dedd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010348"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>Comparar opciones para almacenar objetos Blob (SQL Server)
  Explica y compara las opciones que están disponibles para almacenar archivos y documentos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="Expectations"></a> Almacenamiento de archivos en la base de datos - Ventajas y expectativas  
 Un porcentaje alto de los datos empresariales no se estructuran por naturaleza y se suelen almacenar como archivos y documentos en los sistemas de archivos. Las aplicaciones que tienen acceso a los archivos a través de las API de Windows generan, administran y consumen la mayor parte de los datos. Las empresas suelen mantener estos datos en el sistema de archivos, mientras que almacenan los metadatos relacionados de los archivos en una base de datos relacional.  
  
 Integrar los datos no estructurados en la base de datos relacional proporciona beneficios significativos. Entre estos beneficios, se incluyen los siguientes:  
  
-   Capacidades de almacenamiento integrado y administración de datos como la copia de seguridad.  
  
-   Servicios integrados como la búsqueda de texto completo y la búsqueda semántica en datos y metadatos.  
  
-   Facilidad de administración y administración de directivas en datos no estructurados.  
  
 En su mayor parte, sin embargo, no ha sido cómodo almacenar los datos no estructurados en una base de datos relacional. Hasta ahora no ha sido posible ejecutar las aplicaciones existentes basadas Windows existente en sistemas relacionales. No es práctico volver a escribir aplicaciones establecidas (como Microsoft Word o Adobe Reader) para que se ejecuten en las API de bases de datos relacionales. Estas aplicaciones esperan simplemente que se acceda a los datos a través de las API de Windows. Es decir, las expectativas incluyen:  
  
-   Las aplicaciones Windows no tienen en cuenta las transacciones de la base de datos y no las necesitan.  
  
-   Las aplicaciones Windows requieren compatibilidad con las API del sistema de archivos para los datos de archivos y directorios.  
  
##  <a name="Filestream"></a> FILESTREAM  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya incluye la característica FILESTREAM, que proporciona almacenamiento, administración y transmisión de datos eficaces de los datos no estructurados almacenados como archivos en el sistema de archivos. Sin embargo, una solución FILESTREAM requiere la programación personalizada y no satisface el requisito de compatibilidad completa de las aplicaciones Windows descrito anteriormente.  
  
##  <a name="FileTables"></a> FileTables  
 La característica FileTable se basa en las capacidades existentes de FILESTREAM para habilitar que los clientes de empresa almacenen los datos de archivos no estructurados y las jerarquías de directorio en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , direccionando los requisitos de acceso no transaccional y la compatibilidad de las aplicaciones Windows con datos basados en archivos.  
  
##  <a name="CompareFileTable"></a> Comparar FILESTREAM y FileTable  
  
|Característica|Servidor de archivos y solución de base de datos|Solución de FILESTREAM|Solución de FileTable|  
|-------------|---------------------------------------|-------------------------|------------------------|  
|**Un solo artículo para tareas de administración**|No|Sí|**Sí**|  
|**Un solo conjunto de servicios**: búsquedas, informes, consultas, etc.|No|Sí|**Sí**|  
|**Modelo de seguridad integrada**|Sin|Sí|**Sí**|  
|**Actualizaciones en contexto de datos FILESTREAM**|Sí|Sin|**Sí**|  
|**Jerarquía de archivos y de directorios que se mantiene en la base de datos**|Sin|Sin|**Sí**|  
|**Compatibilidad con aplicaciones Windows**|Sí|Sin|**Sí**|  
|**Acceso relacional a los atributos de archivo**|Sin|No|**Sí**|  
  
##  <a name="CompareRBS"></a> Comparar FILESTREAM y el almacén remoto de BLOBS (RBS)  
 Para obtener una comparación de estas dos características, consulte este blog del equipo RBS: [Comparación de características de SQL Server remoto BLOB Store y FILESTREAM](https://go.microsoft.com/fwlink/?LinkId=210317).  
  
##  <a name="more"></a> Más información  
 [FILESTREAM &#40;SQL Server&#41;](filestream-sql-server.md)  
 [FileTables &#40;SQL Server&#41;](filetables-sql-server.md)  
 [Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](remote-blob-store-rbs-sql-server.md)  
  
