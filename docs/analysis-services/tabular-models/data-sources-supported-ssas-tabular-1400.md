---
title: Orígenes de datos admitidos en modelos tabulares 1400 de Analysis Services de SQL Server | Microsoft Docs
ms.date: 07/02/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 246375015786cf67685c89f368f83662539da36b
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597348"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>Orígenes de datos admiten en SQL Server Analysis Services, los modelos tabulares 1400

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

En este artículo se describe los tipos de orígenes de datos que se pueden usar con modelos tabulares de SQL Server Analysis Services (SSAS) en el nivel de compatibilidad 1400. 

Para los modelos tabulares de SSAS en los niveles de compatibilidad 1200 y versiones inferiores, consulte [orígenes de datos admitidos en modelos tabulares 1200 de SQL Server Analysis Services](data-sources-supported-ssas-tabular.md).

Para Azure Analysis Services, consulte [orígenes de datos admitidos en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).


## <a name="cloud-data-sources"></a>Orígenes de datos en la nube

|Origen de datos  |En la memoria  |DirectQuery  |
|---------|---------|---------|
|Base de datos SQL Azure <sup> [1](#ae)</sup>    |   Sí      |    Sí      |
|Almacenamiento de datos SQL de Azure     |   Sí      |   Sí       |
|Azure Blob Storage     |   Sí       |    No      |
|Azure Table Storage    |   Sí       |    Sin      |
|Azure Cosmos DB     |  Sí        |  Sin        |
|Azure Data Lake Store (Gen1)<sup>[2](#gen2)</sup>      |   Sí       |    Sin      |
|HDFS de HDInsight de Azure    |     Sí     |   Sin       |
|Azure HDInsight Spark <sup> [3](#databricks)</sup>     |   Sí       |   Sin       |
||||

<a name="ae">1</a> -azure SQL Database Always Encrypted no se admite.   
<a name="gen2">2</a> -Gen2 ADLS no se admite actualmente.   
<a name="databricks">3</a> : azure Databricks mediante el conector no se admite actualmente de Spark.   




**Proveedor**   
En la memoria y los modelos DirectQuery conectarse a orígenes de datos de Azure usan .NET Framework Data Provider para SQL Server.

## <a name="on-premises-data-sources"></a>Orígenes de datos locales

### <a name="supported-by-in-memory-and-directquery-models"></a>Compatible con in-memory y los modelos DirectQuery

|Origen de datos | Proveedor en memoria | Proveedor de DirectQuery |
|  --- | --- | --- |
| SQL Server <sup>[4](#aeop)</sup> |SQL Server Native Client 11.0, proveedor Microsoft OLE DB para SQL Server, proveedor de datos de .NET Framework para SQL Server | Proveedor de datos de .NET Framework para SQL Server |
| Almacenamiento de datos SQL Server |SQL Server Native Client 11.0, proveedor Microsoft OLE DB para SQL Server, proveedor de datos de .NET Framework para SQL Server | Proveedor de datos de .NET Framework para SQL Server |
| Oracle |Proveedor Microsoft OLE DB para Oracle, proveedor de datos de Oracle para .NET |Proveedor de datos de Oracle para .NET | |
| Teradata |Proveedor OLE DB para Teradata, proveedor de datos de Teradata para .NET |Proveedor de datos de Teradata para .NET | |
| | | |

<a name="aeop">4</a> -base de datos de azure SQL Database y SQL Server Always Encrypted se admite como DirectQuery [el origen de datos de cliente](data-sources-supported-ssas-tabular.md#bkmk_supported_ds_dq) en los modelos tabulares de SQL Server Analysis Services en el nivel de compatibilidad de 1200 solo. Base de datos de Azure SQL Database y SQL Server Always Encrypted no se admite en Azure Analysis Services.       

> [!NOTE]
> Para los modelos en memoria, los proveedores OLE DB pueden proporcionar un mejor rendimiento para los datos a gran escala. Al elegir entre diferentes proveedores para el mismo origen de datos, pruebe primero el proveedor OLE DB.  

### <a name="supported-by-in-memory-models-only"></a>Admite solo los modelos en memoria

|Base de datos  |
|---------|---------|---------|
|Base de datos de Access     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|Documento JSON     | 
|Líneas del archivo binario     | 
|MySQL Database     | 
|Base de datos de PostgreSQL    | Sí | Sin
|SAP HANA   | Sí | Sin
|SAP Business Warehouse    | Sí | No
|Base de datos de Sybase     | Sí | Sin
|||

|Archivo  |  
|---------|---------|
|Libro de Excel     |
|Carpeta     | 
|JSON | 
|Texto o CSV    | 
|Tabla XML    | 
|||

|Servicios en línea  |  
|---------|---------|
|Dynamics 365      |
|Exchange Online     |
|Objetos de Salesforce    | 
|Informes de Salesforce     |
|Lista de SharePoint Online     |
|||

|Otros  |  
|---------|---------|
|Active Directory      | 
|Exchange     |  
|Fuente de OData     | 
|Consulta ODBC     | 
|OLE DB  | 
|Lista de SharePoint | 
|||

## <a name="see-also"></a>Vea también

[Orígenes de datos compatibles en SQL Server Analysis Services, los modelos tabulares 1200](data-sources-supported-ssas-tabular.md)

[Orígenes de datos admitidos en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
