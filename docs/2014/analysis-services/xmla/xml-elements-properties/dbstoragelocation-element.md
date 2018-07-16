---
title: Elemento DbStorageLocation | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 055780c9c91817a44dce6dfdaeb6ea3b541c05a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224005"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|""|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](database-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `DbStorageLocation` propiedad de base de datos debe establecerse en una ruta UNC de carpeta existente o una cadena vacía. De manera predeterminada, la carpeta de datos del servidor es una cadena vacía. Si la carpeta no existe, se producirá un error al ejecutar un comando `Create`, `Attach` o `Alter`.  
  
 Además, el `DbStorageLocation` no se puede establecer la propiedad de base de datos para que apunte a la carpeta de datos del servidor o a cualquiera de sus subcarpetas. Si la ubicación apunta a la carpeta de datos del servidor o a cualquiera de sus subcarpetas, se producirá un error al ejecutar un `Create`, `Attach`, o `Alter` comando.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
