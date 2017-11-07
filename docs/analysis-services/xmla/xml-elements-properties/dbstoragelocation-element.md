---
title: Elemento DbStorageLocation | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9267f5858eb837efdbcd84fb040934e767835d4f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbstoragelocation-element"></a>Elemento DbStorageLocation
  Especifica la carpeta en la que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea y administra todos los datos de la base de datos y los archivos de metadatos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|""|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 La propiedad de base de datos **DbStorageLocation** se debe establecer en una ruta UNC de carpeta existente o en una cadena vacía. De manera predeterminada, la carpeta de datos del servidor es una cadena vacía. Si la carpeta no existe, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
 Además, la propiedad de base de datos **DbStorageLocation** no se puede establecer para que apunte a la carpeta de datos del servidor ni a ninguna de sus subcarpetas. Si la ubicación apunta a la carpeta de datos del servidor o a cualquiera de sus subcarpetas, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

