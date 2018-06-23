---
title: Propiedades de información del origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 980e7ea889cc8c95828b4c704748aa6dc2552359
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199355"
---
# <a name="data-source-information-properties"></a>Propiedades de información de orígenes de datos
  En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERDATASOURCE, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> L/E: Lectura<br /><br /> Valor predeterminado: VARIANT_TRUE<br /><br /> Descripción: Se utiliza para determinar si se admite la intercalación de columnas.<br /><br /> VARIANT_TRUE: Se admite la intercalación de columnas.<br /><br /> VARIANT_FALSE: No se admite la intercalación de columnas.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 L/E: Lectura<br /><br /> Descripción: Id. de configuración regional de Unicode.<br /><br /> Se trata de la configuración regional utilizada para ordenar datos Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 L/E: Lectura<br /><br /> Descripción: Estilo de comparación Unicode.<br /><br /> Las opciones de ordenación utilizadas para ordenar datos Unicode.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSESSION, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define la propiedad adicional siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR L/E: Lectura/escritura<br /><br /> Descripción: El resultado de una consulta FOR XML podría no ser un documento bien formado. Cuando se especifica esta propiedad, el resultado de un ' Seleccionar... para XML' consulta se incluye en la etiqueta proporcionada por esta propiedad para devolver un documento XML bien formado. Si la consulta se ejecuta en el explorador, puede hacer que el explorador muestre los errores de análisis al cargar el resultado. Para evitar el error, SQL ISAPI admite la palabra clave ROOT. Esta palabra clave se asigna a la propiedad SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  