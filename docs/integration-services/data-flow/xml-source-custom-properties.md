---
title: Propiedades personalizadas del origen XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c37fbff21d10a7eba5ee3f1ce1df55d997379dd2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="xml-source-custom-properties"></a>Propiedades personalizadas del origen XML
  El origen XML tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modo que se usa para tener acceso los datos XML.|  
|UseInlineSchema|Boolean|Valor que indica si se usa una definición de esquema insertada dentro del origen XML. El valor predeterminado de esta propiedad es **False**.|  
|XMLDATA|String|Archivo o variables desde las que recuperar los datos XML.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|XMLSchemaDefinition|String|Ruta de acceso y nombre del archivo de definición de esquema (.xsd).<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de la salida del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Valor que identifica el conjunto de filas asociado a la salida.|  
  
 La salida y las columnas de salida del origen XML no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Ver también  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
