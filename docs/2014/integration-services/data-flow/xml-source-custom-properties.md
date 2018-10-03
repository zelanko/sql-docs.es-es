---
title: Propiedades personalizadas del origen XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6843e2f2d818789a791ba12c78e5aa42a086a15d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224785"
---
# <a name="xml-source-custom-properties"></a>Propiedades personalizadas del origen XML
  El origen XML tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modo que se usa para tener acceso los datos XML.|  
|UseInlineSchema|Boolean|Valor que indica si se usa una definición de esquema insertada dentro del origen XML. El valor predeterminado de esta propiedad es `False`.|  
|XMLDATA|String|Archivo o variables desde las que recuperar los datos XML.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|XMLSchemaDefinition|String|Ruta de acceso y nombre del archivo de definición de esquema (.xsd).<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de la salida del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Valor que identifica el conjunto de filas asociado a la salida.|  
  
 La salida y las columnas de salida del origen XML no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [XML Source](xml-source.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  
