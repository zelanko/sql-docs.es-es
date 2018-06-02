---
title: Elemento DbStorageLocation | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 42b0b7e4ded0aa9d31587e5a4fa296968559e78b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579117"
---
# <a name="dbstoragelocation-element"></a>Elemento DbStorageLocation
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
|Tipo y longitud de los datos|String|  
|Valor predeterminado|""|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Base de datos](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 La propiedad de base de datos **DbStorageLocation** se debe establecer en una ruta UNC de carpeta existente o en una cadena vacía. De manera predeterminada, la carpeta de datos del servidor es una cadena vacía. Si la carpeta no existe, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
 Además, la propiedad de base de datos **DbStorageLocation** no se puede establecer para que apunte a la carpeta de datos del servidor ni a ninguna de sus subcarpetas. Si la ubicación apunta a la carpeta de datos del servidor o a cualquiera de sus subcarpetas, se producirá un error al ejecutar un comando **Create**, **Attach**o **Alter** .  
  
## <a name="see-also"></a>Vea también
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
