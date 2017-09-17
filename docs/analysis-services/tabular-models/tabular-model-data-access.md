---
title: Acceso a datos de modelo tabular | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4763973d0ea4bf905b1c38ace337667c92186e3a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-model-data-access"></a>Acceso a datos de modelos tabulares
  A las bases de datos modelo tabulares de Analysis Services se puede tener acceso con la mayoría de los clientes, interfaces e idiomas que se usan para recuperar los datos o metadatos de un modelo multidimensional. Para más información, vea [Acceso a datos de modelos multidimensionales &#40;Analysis Services: datos multidimensionales&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 En este tema se describen los clientes, los lenguajes de consulta y las interfaces de programación que funcionan con modelos tabulares.  
  
## <a name="clients"></a>Clientes  
 Las aplicaciones cliente siguientes de Microsoft admiten conexiones nativas a las bases de datos de modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
### <a name="power-bi"></a>Power BI
Se puede conectar a una base de datos de modelo tabular de Analysis Services local desde [Power BI](https://powerbi.microsoft.com/). Power BI es un conjunto de herramientas de análisis empresarial para analizar datos y compartir información. 

### <a name="excel"></a>Excel  
 Puede conectarse a bases de datos de modelos tabulares de Excel, utilizando las capacidades de visualización y análisis de los datos en Excel para trabajar con los datos. Para tener acceso a los datos, defina una conexión de datos de Analysis Services, especifique un servidor que se ejecute en modo de servidor tabular y elija la base de datos que desea utilizar. Para obtener más información, vea [Conectarse a datos o importarlos desde SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
 Excel también es la aplicación recomendada para examinar modelos tabulares en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. La herramienta incluye una opción **Analizar en Excel** que inicia una nueva instancia de Excel, crea un libro de Excel y abre una conexión de datos del libro con la base de datos del área de trabajo del modelo. Al examinar datos de modelo tabulares en Excel, tenga en cuenta que Excel emite consultas en el modelo utilizando el cliente de tablas dinámicas de Excel. En consecuencia, las operaciones en el libro de Excel dan lugar a que se envíen consultas MDX a la base de datos del área de trabajo, en lugar de consultas DAX. Si utiliza SQL Server profiler u otra herramienta de supervisión para supervisar consultas, puede suceder que vea MDX y no DAX en el seguimiento del analizador. Para más información sobre la característica Analizar en Excel, vea [Analizar en Excel &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] es una aplicación cliente de informes de Reporting Services que se ejecuta en un entorno de SharePoint 2010. Combina la exploración de datos, el diseño de la consulta, y el diseño de la presentación en una experiencia ad hoc integrada de informes. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] puede utilizar modelos tabulares como orígenes de datos, independientemente de si el modelo está hospedado en una instancia de Analysis Services que se ejecuta en modo tabular o se recupera de un almacén de datos relacional con el modo DirectQuery. Para conectarse a un modelo tabular en [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], debe crear un archivo de conexión que contenga la ubicación del servidor y el nombre de la base de datos. Puede crear un origen de datos compartido de Reporting Services o un archivo de conexión de modelo semántico de BI en SharePoint. Para más información sobre las conexiones de modelos semánticos de BI, vea [Conexión del modelo semántico de BI de Power Pivot &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md).  
  
 El cliente [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] determina la estructura del modelo especificado enviando una solicitud al origen de datos especificado, que devuelve un esquema que puede ser utilizado por el cliente para crear consultas en el modelo como origen de datos y para realizar operaciones basadas en los datos. Las operaciones posteriores de la interfaz de usuario de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para filtrar los datos, realizar cálculos o agregaciones, y mostrar los datos asociados son controlados por el cliente y no se pueden controlar mediante programación.  
  
 Las consultas que el cliente [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] envía al modelo se generan como instrucciones DAX, que puede supervisarse estableciendo un seguimiento en el modelo.  El cliente también emite una solicitud al servidor pidiendo la definición de esquema inicial, que se muestra según el lenguaje de definición de esquemas conceptuales (CSDL). Para más información, vea [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Puede utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar las instancias que hospedan modelos tabulares y para consultar los metadatos y los datos que contienen. Puede procesar los modelos o los objetos de un modelo, crear y administrar las particiones, y establecer la seguridad que se puede utilizar para administrar el acceso a los datos. Para obtener más información, consulte los temas siguientes:  
  
-   [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
-   [Supervisar una instancia de Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
 Puede utilizar las ventanas de consulta MDX y XMLA en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para recuperar datos y metadatos de una base de datos de modelo tabular. Sin embargo, tenga en cuenta que existen las siguientes restricciones:  
  
-   Las instrucciones que usan MDX y DMX no se admiten para los modelos que se han implementado en modo DirectQuery; por consiguiente, si necesita crear una consulta en un modelo tabular en el modo DirectQuery, debe utilizar una ventana de **Consulta XMLA** en su lugar.  
  
-   No puede cambiar el contexto de la base de datos de la ventana de consulta XMLA una vez abierta la ventana de **Consulta** . Por consiguiente, si necesita enviar una consulta a una base de datos o a una instancia diferentes, debe abrir la base de datos o la instancia con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y abrir una nueva ventana de **Consulta XMLA** dentro del contexto.  
  
 Puede crear seguimientos en un modelo tabular de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] igual que en una solución multidimensional. En esta versión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona muchos eventos nuevos que se pueden utilizar para realizar el seguimiento de las operaciones de procesamiento, consulta y uso de la memoria, así como el uso de los archivos. Para más información, vea [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md).  
  
> [!WARNING]  
>  Si coloca un seguimiento en una base de datos de modelo tabular, podría ver algunos eventos que se clasifican como consultas DMX. Sin embargo, la minería de datos no se admite en los datos de modelos tabulares y las consultas DMX ejecutadas en la base de datos se limitan a las instrucciones SELECT en los metadatos del modelo. Los eventos se clasifican como DMX solo porque para MDX se usa el mismo marco de trabajo del analizador.  
  
## <a name="query-languages"></a>Lenguajes de consulta  
 Los modelos tabulares de Analysis Services admiten la mayor parte de los mismos lenguajes de consulta que se proporcionan para el acceso a los modelos multidimensionales. La excepción son los modelos tabulares que se han implementado en modo DirectQuery, que no recuperan los datos de un almacén de datos de Analysis Services sino directamente de un origen de datos de SQL Server. No se pueden consultar estos modelos con MDX, sino que es necesario usar un cliente que admita la conversión de las expresiones DAX en instrucciones Transact-SQL, como el cliente [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
### <a name="dax"></a>DAX  
 Puede usar DAX para crear expresiones y fórmulas en todos los tipos de modelos tabulares, independientemente de si el modelo se almacena en SharePoint como un libro de Excel habilitado para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]o en una instancia de Analysis Services.  
  
 Además, puede utilizar expresiones DAX dentro del contexto de una instrucción de comando EXECUTE XMLA para enviar consultas a un modelo tabular que se haya implementado en el modo DirectQuery.  
  
 Para obtener ejemplos de consultas en un modelo tabular con DAX, vea [Referencia de la sintaxis de las consultas DAX](http://msdn.microsoft.com/en-us/4dd0cf0e-191d-411d-987c-f606813fc39e).  
  
### <a name="mdx"></a>MDX  
 Puede utilizar MDX para crear consultas en modelos tabulares que usen la memoria caché en memoria como método preferido de consulta (es decir, los modelos que no se hayan implementado en modo DirectQuery). Aunque los clientes como [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] usan DAX tanto para crear agregaciones como para consultar el modelo como un origen de datos, si conoce MDX, puede ser una forma rápida de crear consultas de ejemplo en MDX (vea [Generar medidas en MDX](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)).  
  
### <a name="csdl"></a>CSDL  
 El lenguaje de definición de esquemas conceptuales (CSDL) no es un lenguaje de consulta en sí mismo, pero se puede utilizar para recuperar información sobre el modelo y los metadatos del modelo, que se pueden utilizar posteriormente para crear informes o consultas para el modelo.  
  
 Para obtener información sobre cómo se usa CSDL en modelos tabulares, vea [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="programmatic-interfaces"></a>Interfaces de programación  
 Las interfaces principales que se utilizan para interactuar con los modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son los conjuntos de filas de esquema, XMLA y los clientes de consultas, así como las herramientas de consulta que proporcionan [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
### <a name="data-and-metadata"></a>Datos y metadatos  
 Puede recuperar datos y metadatos de modelos tabulares en aplicaciones administradas mediante ADOMD.NET. 
  
-   [Usar vistas de administración dinámica &#40;DMV&#41; para supervisar Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 Puede usar el proveedor OLE DB 9.0 para Analysis Services en aplicaciones cliente sin administrar para admitir el acceso OLE DB a los modelos tabulares. Se requiere una versión actualizada del proveedor OLE DB de Analysis Services para habilitar el acceso al modelo tabular. Para más información sobre los proveedores utilizados con los modelos tabulares, vea [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) .  
  
 También puede recuperar los datos directamente desde una instancia de Analysis Services en un formato basado en XML. Puede recuperar el esquema del modelo tabular utilizando el conjunto de filas DISCOVER_CSDL_METADATA o puede utilizar un comando EXECUTE o DISCOVER con las propiedades, objetos o elementos ASSL existentes. Para obtener más información, vea los recursos siguientes:  
  
-   [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="manipulate-analysis-services-objects"></a>Manipular objetos de Analysis Services  
 Puede crear, modificar, eliminar y procesar los modelos tabulares y los objetos contenidos en ellos, como tablas, columnas, perspectivas, medidas y particiones, mediante comandos XMLA o mediante AMO. Tanto AMO como XMLA se han actualizado para admitir las propiedades adicionales que se utilizan en los modelos tabulares para mejorar los informes y el modelado.  
  
  
### <a name="schema-rowsets"></a>Conjuntos de filas de esquema  
 Las aplicaciones cliente pueden utilizar conjuntos de filas de esquema para examinar los metadatos de los modelos tabulares y recuperar la información de supervisión y soporte técnico del servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . En esta versión de SQL Server, se han agregado nuevos conjuntos de filas de esquema y los conjuntos de filas de esquema existentes se han ampliado para admitir características relacionadas con los modelos tabulares y mejorar el análisis del rendimiento y la supervisión mediante [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   [DISCOVER_CALC_DEPENDENCY, conjunto de filas](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)  
  
     Nuevo conjunto de filas de esquema para el seguimiento de dependencias entre columnas y referencias en un modelo tabular  
  
-   [DISCOVER_CSDL_METADATA, conjunto de filas](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)  
  
     Nuevo conjunto de filas de esquema para obtener la representación CSDL de un modelo tabular  
  
-   [Conjunto de filas DISCOVER_XEVENT_TRACE_DEFINITION](http://msdn.microsoft.com/library/e1ce2d2d-f994-4318-801a-ee0385aecd84)  
  
     Nuevo conjunto de filas de esquema para supervisar Eventos extendidos de SQL Server. Para más información, vea [Supervisar Analysis Services con SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
-   [Conjunto de filas DISCOVER_TRACES](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)  
  
     La nueva columna **Type** permite filtrar los seguimientos por categoría. Para más información, vea [Crear seguimientos del generador de perfiles para su reproducción &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
-   [Conjunto de filas MDSCHEMA_HIERARCHIES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)  
  
     La nueva enumeración de **STRUCTURE_TYPE** admite la identificación de las jerarquías definidas por el usuario creadas en los modelos tabulares. Para más información, vea [Jerarquías &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
 En esta versión, no hay actualizaciones de OLE DB para los conjuntos de filas de esquema de minería de datos.  
  
> [!WARNING]  
>  No pueden utilizar consultas DMX o MDX en una base de datos que se haya implementado en el modo DirectQuery; por consiguiente, si necesita ejecutar una consulta en un modelo DirectQuery con conjuntos de filas de esquema, debe usar XMLA y no el DMV asociado. Para los DMV que devuelven resultados del servidor como un todo, como SELECT * from $system.DBSCHEMA_CATALOGS o DISCOVER_TRACES, puede ejecutar la consulta en el contenido de una base de datos que se implemente en un modo de caché.  
  
## <a name="see-also"></a>Vea también  
 [Conectar a una base de datos de modelo tabular &#40;SSAS&#41;](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)   
 [Acceso a datos de Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-access.md)   
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
