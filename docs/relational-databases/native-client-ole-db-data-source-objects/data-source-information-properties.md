---
title: Propiedades de información de orígenes de datos | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e732ffc43f0728cf884761997c1006e290304c91
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002778"
---
# <a name="data-source-information-properties"></a>Propiedades de información de orígenes de datos
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERDATASOURCE, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Escriba:  VT_BOOL<br /><br /> L/E: Lectura<br /><br /> Valor predeterminado: VARIANT_TRUE<br /><br /> Descripción: Se utiliza para determinar si se admite la intercalación de columnas.<br /><br /> VARIANT_TRUE: Se admite la intercalación de columnas.<br /><br /> VARIANT_FALSE: No se admite la intercalación de columnas.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 L/E: Lectura<br /><br /> Descripción: Id. de configuración regional de Unicode.<br /><br /> Se trata de la configuración regional utilizada para ordenar datos Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 L/E: Lectura<br /><br /> Descripción: Estilo de comparación Unicode.<br /><br /> Las opciones de ordenación utilizadas para ordenar datos Unicode.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSESSION, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define la propiedad adicional siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR L/E: Lectura/escritura<br /><br /> Descripción: El resultado de una consulta FOR XML podría no ser un documento bien formado. Cuando se especifica esta propiedad, se incluye el resultado de una consulta 'select ... for XML' en la etiqueta proporcionada por la propiedad para devolver un documento XML bien formado. Si la consulta se ejecuta en el explorador, puede hacer que el explorador muestre los errores de análisis al cargar el resultado. Para evitar el error, SQL ISAPI admite la palabra clave ROOT. Esta palabra clave se asigna a la propiedad SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte también  
 [Objetos de origen de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
