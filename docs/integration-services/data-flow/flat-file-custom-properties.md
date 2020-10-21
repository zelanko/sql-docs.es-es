---
description: Propiedades personalizadas de archivo plano
title: Propiedades personalizadas de archivo plano | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 06e9cacfa5514648fc69bff0148a4448af536de0
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194215"
---
# <a name="flat-file-custom-properties"></a>Propiedades personalizadas de archivo plano

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Propiedades personalizadas de origen**  
  
 El origen de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|Nombre de una columna de salida que contiene el nombre de archivo. Si no se especifica ningún nombre, se generará ninguna columna de salida que contenga el nombre de archivo.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
|RetainNulls|Boolean|Valor que especifica si retener los valores Null del archivo de origen como tales cuando el motor de canalización de transformación de datos procesa los datos. El valor predeterminado de esta propiedad es **False**.|  
  
 La salida del origen de archivo plano no tiene ninguna propiedad personalizada.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Valor que indica si la columna usa las rutinas de análisis más rápidas que no distinguen la configuración regional y permiten un análisis rápido que DTS proporciona, o las rutinas de análisis estándar que sí distinguen la configuración regional. Para obtener más información, consulte [Fast Parse](./parsing-data.md) y [Standard Parse](./parsing-data.md). El valor predeterminado de esta propiedad es **False**.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
  
 Para más información, consulte [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Encabezado|String|Bloque de texto que se inserta en el archivo antes de que se escriban datos.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|Sobrescribir|Boolean|Valor que especifica si sobrescribir o anexar a un archivo de destino existente que tiene el mismo nombre. El valor predeterminado de esta propiedad es **True**.|  
  
 La entrada y las columnas de entrada del destino de archivo plano no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
