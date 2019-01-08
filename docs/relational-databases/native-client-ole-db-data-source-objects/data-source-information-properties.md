---
title: Propiedades de información del origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5454f7c41a55442c8b68cd57dd71c3859902be97
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535111"
---
# <a name="data-source-information-properties"></a>Propiedades de información de orígenes de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERDATASOURCE, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> R/W: Lectura<br /><br /> Predeterminado: VARIANT_TRUE<br /><br /> Descripción: Se usa para determinar si se admite la intercalación de columna.<br /><br /> VARIANT_TRUE: Se admite la intercalación de columna.<br /><br /> VARIANT_FALSE: No se admite la intercalación de columnas.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 L/E Lectura<br /><br /> Descripción: Id. de configuración regional Unicode.<br /><br /> Se trata de la configuración regional utilizada para ordenar datos Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 L/E Lectura<br /><br /> Descripción: Estilo de comparación Unicode.<br /><br /> Las opciones de ordenación utilizadas para ordenar datos Unicode.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSESSION, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define la propiedad adicional siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR L/E Lectura/escritura<br /><br /> Descripción: El resultado de una consulta FOR XML no puede ser un documento con formato correcto. Cuando se especifica esta propiedad, se ajusta el resultado de una consulta 'select... for XML' en la etiqueta proporcionada por esta propiedad para devolver un documento XML bien formado. Si la consulta se ejecuta en el explorador, puede hacer que el explorador muestre los errores de análisis al cargar el resultado. Para evitar el error, SQL ISAPI admite la palabra clave ROOT. Esta palabra clave se asigna a la propiedad SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
