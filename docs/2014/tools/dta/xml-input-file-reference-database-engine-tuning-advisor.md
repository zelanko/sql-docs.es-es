---
title: Referencia del archivo de entrada XML (Asistente para la optimización de motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b560b36eb98ec73723a4ce25cb3c647f4962b634
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509987"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Referencia del archivo de entrada XML (Asistente para la optimización de motor de base de datos)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede utilizar un archivo de entrada XML para optimizar una base de datos. Este archivo XML designa las bases de datos, las tablas, los archivos o las tablas de carga de trabajo y las opciones de optimización que se van a utilizar durante la sesión de optimización. También se puede utilizar este archivo para definir una configuración especificada por el usuario para realizar análisis de escenarios condicionales.  
  
 Un archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene una jerarquía de elementos XML. Cada uno de estos contiene texto u otros elementos que especifican la configuración de la sesión de optimización. El archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe ajustarse a los estándares de formato XML correcto, de modo que todos los nombres de elemento distingan entre mayúsculas y minúsculas. Los elementos se especifican siguiendo el formato Pascal: el primer carácter y la primera letra de cualquier palabra concatenada siguiente van en mayúsculas.  
  
 Todos los valores de los elementos deben ajustarse a las convenciones de nomenclatura XML. Para obtener más información acerca de estas convenciones, vea el artículo sobre [contenido de texto XML](https://go.microsoft.com/fwlink/?LinkId=7614) en Microsoft MSDN Library.  
  
 Tenga en cuenta que esta referencia no es completa. Para obtener más información acerca de los elementos que se pueden utilizar para definir una entrada XML, vea el esquema XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , DTASchema.xsd.  
  
## <a name="xml-declaration"></a>Declaración XML  
  
-   [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento raíz DTAXML  
  
-   [Elemento DTAXML &#40;DTA&#41;](dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementos DTAInput  
  
-   [Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)  
  
-   [Server &#40;DTA, elemento&#41;](server-element-dta.md)  
  
-   [Workload &#40;DTA, elemento&#41;](workload-element-dta.md)  
  
-   [Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)  
  
-   [Elemento Configuration &#40;DTA&#41;](configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementos Server  
  
-   [Elemento Name de Server &#40;DTA&#41;](name-element-for-server-dta.md)  
  
-   [Elemento Database de Server &#40;DTA&#41;](database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementos Workload  
  
-   [Elemento File &#40;DTA&#41;](file-element-dta.md)  
  
-   [Database &#40;DTA, elemento de Workload&#41;](database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40;DTA&#41;](eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementos de opciones de optimización  
  
-   [Elemento TuningTimeInMin &#40;DTA&#41;](tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40;DTA&#41;](storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40;DTA&#41;](testserver-element-dta.md)  
  
-   [FeatureSet &#40;DTA, elemento&#41;](featureset-element-dta.md)  
  
-   [Partitioning &#40;DTA, elemento&#41;](partitioning-element-dta.md)  
  
-   [DropOnlyMode &#40;DTA, elemento&#41;](droponlymode-element-dta.md)  
  
-   [KeepExisting &#40;DTA, elemento&#41;](keepexisting-element-dta.md)  
  
-   [OnlineIndexOperation &#40;DTA, elemento&#41;](onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40;DTA&#41;](databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementos Configuration  
  
-   [Server &#40;DTA, elemento de Configuration&#41;](server-element-for-configuration-dta.md)  
  
-   [Elemento Database de Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md)  
  
-   [Elemento Recommendation &#40;DTA&#41;](recommendation-element-dta.md)  
  
-   [Create &#40;DTA, elemento&#41;](create-element-dta.md)  
  
-   [Index &#40;DTA, elemento&#41;](index-element-dta.md)  
  
-   [Name &#40;DTA, elemento de Index&#41;](name-element-for-index-dta.md)  
  
-   [Column &#40;DTA, elemento de Index&#41;](column-element-for-index-dta.md)  
  
-   [Elemento Name de Column &#40;DTA&#41;](name-element-for-column-dta.md)  
  
-   [Filegroup &#40;DTA. elemento de Index&#41;](filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementos Database  
  
-   [Elemento Name de Database &#40;DTA&#41;](name-element-for-database-dta.md)  
  
-   [Elemento Schema de Database &#40;DTA&#41;](schema-element-for-database-dta.md)  
  
-   [Elemento Name de Schema &#40;DTA&#41;](name-element-for-schema-dta.md)  
  
-   [Elemento Table de Schema &#40;DTA&#41;](table-element-for-schema-dta.md)  
  
-   [Elemento Name de Table &#40;DTA&#41;](name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Vea también  
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
