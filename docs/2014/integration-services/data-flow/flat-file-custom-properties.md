---
title: Propiedades personalizadas de archivo plano | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fc3fee533b8e4aa8293c5ea6c19c27ef7ef3ed2b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197212"
---
# <a name="flat-file-custom-properties"></a>Propiedades personalizadas de archivo plano
  **Propiedades personalizadas de origen**  
  
 El origen de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|Nombre de una columna de salida que contiene el nombre de archivo. Si no se especifica ningún nombre, se generará ninguna columna de salida que contenga el nombre de archivo.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
|RetainNulls|Boolean|Valor que especifica si retener los valores Null del archivo de origen como tales cuando el motor de canalización de transformación de datos procesa los datos. El valor predeterminado de esta propiedad es `False`.|  
  
 La salida del origen de archivo plano no tiene ninguna propiedad personalizada.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Valor que indica si la columna usa las rutinas de análisis más rápidas que no distinguen la configuración regional y permiten un análisis rápido que DTS proporciona, o las rutinas de análisis estándar que sí distinguen la configuración regional. Para obtener más información, consulte [Fast Parse](../fast-parse.md) y [Standard Parse](../standard-parse.md). El valor predeterminado de esta propiedad es `False`.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
  
 Para más información, consulte [Flat File Source](flat-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Encabezado|String|Bloque de texto que se inserta en el archivo antes de que se escriban datos.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|Sobrescribir|Boolean|Valor que especifica si sobrescribir o anexar a un archivo de destino existente que tiene el mismo nombre. El valor predeterminado de esta propiedad es `True`.|  
  
 La entrada y las columnas de entrada del destino de archivo plano no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Flat File Destination](flat-file-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  