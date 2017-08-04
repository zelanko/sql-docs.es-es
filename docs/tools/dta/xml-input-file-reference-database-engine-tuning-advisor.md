---
title: "Referencia (Asistente para la optimización de motor de base de datos) del archivo de entrada XML | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d98a6bfc0fc61d76c434f20609205c52c202a257
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Referencia del archivo de entrada XML (Asistente para la optimización de motor de base de datos)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]Asistente para la optimización puede utilizar un archivo de entrada XML para optimizar una base de datos. Este archivo XML designa las bases de datos, las tablas, los archivos o las tablas de carga de trabajo y las opciones de optimización que se van a utilizar durante la sesión de optimización. También se puede utilizar este archivo para definir una configuración especificada por el usuario para realizar análisis de escenarios condicionales.  
  
 Un archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene una jerarquía de elementos XML. Cada uno de estos contiene texto u otros elementos que especifican la configuración de la sesión de optimización. El archivo de entrada XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe ajustarse a los estándares de formato XML correcto, de modo que todos los nombres de elemento distingan entre mayúsculas y minúsculas. Los elementos se especifican siguiendo el formato Pascal: el primer carácter y la primera letra de cualquier palabra concatenada siguiente van en mayúsculas.  
  
 Todos los valores de los elementos deben ajustarse a las convenciones de nomenclatura XML. Para obtener más información acerca de estas convenciones, vea el artículo sobre [contenido de texto XML](http://go.microsoft.com/fwlink/?LinkId=7614) en Microsoft MSDN Library.  
  
 Tenga en cuenta que esta referencia no es completa. Para obtener más información acerca de los elementos que se pueden utilizar para definir una entrada XML, vea el esquema XML del Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , DTASchema.xsd.  
  
## <a name="xml-declaration"></a>Declaración XML  
  
-   [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento raíz DTAXML  
  
-   [Elemento DTAXML &#40; DTA &#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementos DTAInput  
  
-   [Elemento DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Elemento Server &#40; DTA &#41;](../../tools/dta/server-element-dta.md)  
  
-   [Workload, elemento &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)  
  
-   [Tuningoptions, elemento &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Elemento de configuración &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementos Server  
  
-   [Elemento de nombre de servidor &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Elemento de la base de datos de servidor &#40; DTA &#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementos Workload  
  
-   [Elemento File &#40; DTA &#41;](../../tools/dta/file-element-dta.md)  
  
-   [Elemento de la base de datos de carga de trabajo &#40; DTA &#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40; DTA &#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementos de opciones de optimización  
  
-   [Elemento TuningTimeInMin &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40; DTA &#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [FeatureSet, elemento &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Creación de particiones elemento &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [Droponlymode, elemento &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [KeepExisting, elemento &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [Onlineindexoperation, elemento &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40; DTA &#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementos Configuration  
  
-   [Elemento de servidor de configuración &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Elemento de la base de datos de configuración &#40; DTA &#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Elemento Recommendation &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Crear elemento &#40; DTA &#41;](../../tools/dta/create-element-dta.md)  
  
-   [Index, elemento &#40; DTA &#41;](../../tools/dta/index-element-dta.md)  
  
-   [Name, elemento de Index &#40; DTA &#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Elemento de columna de índice &#40; DTA &#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Elemento de nombre de columna &#40; DTA &#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Elemento de grupo de archivos de índice &#40; DTA &#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementos Database  
  
-   [Elemento de nombre de base de datos &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Elemento de esquema de base de datos &#40; DTA &#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Elemento Name de Schema &#40; DTA &#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Elemento de tabla de esquema &#40; DTA &#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Elemento de nombre de tabla &#40; DTA &#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Vea también  
 [Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
