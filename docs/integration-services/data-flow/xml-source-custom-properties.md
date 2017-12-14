---
title: Propiedades personalizadas del origen XML | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 71715e49538a68100b73a7a7fe310db9a17386d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="xml-source-custom-properties"></a>Propiedades personalizadas del origen XML
  El origen XML tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modo que se usa para tener acceso los datos XML.|  
|UseInlineSchema|Boolean|Valor que indica si se usa una definición de esquema insertada dentro del origen XML. El valor predeterminado de esta propiedad es **False**.|  
|XMLDATA|String|Archivo o variables desde las que recuperar los datos XML.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|XMLSchemaDefinition|String|Ruta de acceso y nombre del archivo de definición de esquema (.xsd).<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
  
 En la tabla siguiente se describen las propiedades personalizadas de la salida del origen XML. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Valor que identifica el conjunto de filas asociado a la salida.|  
  
 La salida y las columnas de salida del origen XML no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
