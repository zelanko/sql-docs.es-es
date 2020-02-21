---
title: Propiedades de información de orígenes de datos | Microsoft Docs
description: Propiedades de información de orígenes de datos
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ba9fa21f0c22c342922946a43124216a25ba09ef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68016035"
---
# <a name="data-source-information-properties"></a>Propiedades de información de orígenes de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERDATASOURCEINFO, el controlador OLE DB para SQL Server define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Escriba:  VT_BOOL<br /><br /> R (lectura) y W (escritura): Lectura<br /><br /> Valor predeterminado: VARIANT_TRUE<br /><br /> Descripción: Se utiliza para determinar si se admite la intercalación de columnas.<br /><br /> VARIANT_TRUE: Se admite la intercalación de columnas.<br /><br /> VARIANT_FALSE: No se admite la intercalación de columnas.|  
|SSPROP_UNICODELCID|Escriba:  VT_I4 R/W: Lectura<br /><br /> Descripción: Id. de configuración regional Unicode.<br /><br /> Se trata de la configuración regional utilizada para ordenar datos Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Escriba:  VT_I4 R/W: Lectura<br /><br /> Descripción: Estilo de comparación Unicode.<br /><br /> Las opciones de ordenación utilizadas para ordenar datos Unicode.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSTREAM, el controlador OLE DB para SQL Server define la propiedad adicional siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Escriba:  VT_BSTR R/W: Lectura/Escritura<br /><br /> Descripción: El resultado de una consulta FOR XML podría no ser un documento bien formado. Cuando se especifica esta propiedad, se incluye el resultado de una consulta 'select ... for XML' en la etiqueta proporcionada por la propiedad para devolver un documento XML bien formado. Si la consulta se ejecuta en el explorador, puede hacer que el explorador muestre los errores de análisis al cargar el resultado. Para evitar el error, SQL ISAPI admite la palabra clave ROOT. Esta palabra clave se asigna a la propiedad SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Consulte también  
 [Objetos de origen de datos (OLE DB)](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
