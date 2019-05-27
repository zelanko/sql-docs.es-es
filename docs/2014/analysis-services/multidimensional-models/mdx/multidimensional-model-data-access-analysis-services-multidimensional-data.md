---
title: Acceso a datos de modelos multidimensionales (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9e3db19179e74b20837f58602a236721debc18b2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073836"
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>Acceso a datos de modelos multidimensionales (Analysis Services: datos multidimensionales)
  Utilice la información de este tema para aprender a acceder a los datos multidimensionales de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] empleando métodos de programación, script o aplicaciones cliente que incluyan compatibilidad integrada para la conexión a un servidor de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en la red.  
  
 Este tema contiene las siguientes secciones:  
  
 [Aplicaciones cliente](#bkmk_clientapps)  
  
 [Lenguajes de consulta](#bkmk_querylang)  
  
 [Interfaces de programación](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a> Aplicaciones cliente  
 Aunque Analysis Services proporciona interfaces que permiten generar o integrar bases de datos multidimensionales mediante programación, un enfoque más habitual consiste en utilizar aplicaciones cliente existentes de Microsoft y otros fabricantes de software que tienen acceso de datos integrados a datos de Analysis Services.  
  
 Las aplicaciones de Microsoft siguientes admiten conexiones nativas a datos multidimensionales.  
  
### <a name="excel"></a>Excel  
 Los datos multidimensionales de Analysis Services se suelen presentar usando controles de tablas dinámicas y gráficos dinámicos en un libro de Excel. Las tablas dinámicas son apropiadas para los datos multidimensionales porque las jerarquías, las agregaciones, y las construcciones de navegación del modelo se combinan bien con las características de resumen de datos de una tabla dinámica. En una instalación de Excel se incluye un proveedor de datos OLE DB de Analysis Services para facilitar la configuración de las conexiones de datos. Para obtener más información, vea [Conectarse a datos o importarlos desde SQL Server Analysis Services](https://go.microsoft.com/fwlink/?linkID=215150).  
  
### <a name="reporting-services-reports"></a>Informes de Reporting Services  
 Puede utilizar el Generador de informes o el Diseñador de informes para crear informes que utilicen bases de datos de Analysis Services que contengan datos analíticos. El Generador de informes y el Diseñador de informes incluyen un diseñador de consultas MDX que se puede utilizar para escribir o diseñar instrucciones MDX que recuperen datos de un origen de datos disponible. Para obtener más información, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) y [Tipo de conexión de Analysis Services para MDX &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md).  
  
### <a name="performancepoint-dashboards"></a>Paneles de PerformancePoint  
 Los paneles de PerformancePoint se utilizan para crear tarjetas de puntuación en SharePoint que comuniquen el rendimiento empresarial en función de medidas predefinidas. PerformancePoint incluye compatibilidad con conexiones de datos a datos multidimensionales de Analysis Services. Para obtener más información, vea [Creación de una conexión de datos de Analysis Services (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkid=232471).  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 Los diseñadores de modelos y de informes utilizan las herramientas de de datos de SQL Server para generar soluciones que incluyen modelos multidimensionales. La implementación de la solución en una instancia de Analysis Services es lo que crea la base de datos a la que se conecta posteriormente desde Excel, Reporting Services y otras aplicaciones cliente de Business Intelligence.  
  
 SQL Server Data Tools se generan en un shell de Visual Studio y usan proyectos para organizar y contener el modelo. Para obtener más información, vea [Crear modelos multidimensionales al usar las herramientas de datos de SQL Server &#40;SSDT&#41;](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md).  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Para los administradores de bases de datos, SQL Server Management Studio es un entorno integrado para administrar las instancias de SQL Server, por ejemplo instancias de Analysis Services y bases de datos multidimensionales. Para obtener más información, vea [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) y [Conectar a Analysis Services](../../instances/connect-to-analysis-services.md).  
  
##  <a name="bkmk_querylang"></a> Lenguajes de consulta  
 MDX es un lenguaje de cálculo y consulta estándar del sector que se utiliza para recuperar datos de bases de datos OLAP. En Analysis Services, MDX es el lenguaje de consulta que se utiliza para recuperar datos, pero también admite la definición de datos y la manipulación de datos. Los editores MDX se integran en SQL Server Management Studio, Reporting Services y las herramientas de datos de SQL Server. Puede utilizar los editores MDX para crear consultas ad hoc o script reutilizable si la operación de datos es repetible.  
  
 Algunas herramientas y aplicaciones, como Excel, usan construcciones MDX internamente para consultar un origen de datos de Analysis Services. También se puede utilizar MDX mediante programación, incluyendo la instrucción MDX en un solicitud Execute de XMLA.  
  
 Los siguientes vínculos proporcionan más información acerca de MDX:  
  
 [Consultar datos multidimensionales con MDX](querying-multidimensional-data-with-mdx.md)  
  
 [Conceptos clave de MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a> Interfaces de programación  
 Si está generando una aplicación personalizada que usa datos multidimensionales, el enfoque para tener acceso a los datos entrará muy probablemente en una de las siguientes categorías:  
  
-   **XMLA**. Utilice XMLA cuando se requiera compatibilidad con gran variedad de sistemas operativos y protocolos. XMLA proporciona la máxima flexibilidad, pero suele ser a costa de la mejora de rendimiento y de la facilidad de programación.  
  
-   **Bibliotecas de cliente** Utilice las bibliotecas de cliente de Analysis Services, como ADOMD.NET, AMO y OLE DB cuando desee obtener acceso mediante programación a datos de aplicaciones cliente que se ejecutan en un sistema operativo Microsoft Windows. Las bibliotecas de cliente encapsulan XMLA con un modelo de objetos y optimizaciones que proporcionan un mejor rendimiento.  
  
     Las bibliotecas de cliente de ADOMD.NET y AMO son para aplicaciones escritas en código administrado. Utilice OLE DB para Analysis Services si la aplicación está escrita en código nativo.  
  
 La tabla siguiente proporciona detalles y vínculos adicionales sobre las bibliotecas de cliente que se utilizan para conectar Analysis Services con una aplicación personalizada.  
  
|Interfaz|Descripción|  
|---------------|-----------------|  
|Objetos de administración de Analysis Services (AMO)|AMO es el modelo de objetos principal para administrar instancias de Analysis Services y bases de datos multidimensionales en código. Por ejemplo, SQL Server Management Studio utiliza AMO para admitir la administración de servidor y de base de datos. Para obtener más información, vea [Desarrollar con Objetos de administración de análisis &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).|  
|ADOMD.NET|ADOMD.NET es el modelo de objetos principal para crear y acceder a datos multidimensionales en aplicaciones personalizadas. Puede utilizar ADOMD.NET en una aplicación cliente administrada para recuperar información de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con las interfaces de acceso a datos de Microsoft .NET Framework más habituales. Para obtener más información, vea [Desarrollar con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) y [Programación del cliente ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming).|  
|Proveedor OLE DB de Analysis Services (MSOLAP.dll)|Puede utilizar el proveedor OLE DB nativo para tener acceso a [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] mediante programación desde una API no-administrada. Para obtener más información, vea [Proveedor OLE DB de Analysis Services &#40;Analysis Services - Datos multidimensionales&#41;](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md).|  
|Conjuntos de filas de esquema|Las tablas del conjunto de filas de esquema son estructuras de datos que contienen información descriptiva sobre un modelo multidimensional que se implementa en el servidor, así como información sobre la actividad actual en el servidor. Como programador, puede consultar tablas del conjunto de filas de esquema en aplicaciones cliente para examinar los metadatos almacenados en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y recuperar de dicha instancia información de soporte técnico y de supervisión. Puede usar los conjuntos de filas de esquema con estas interfaces de programación: OLE DB, OLE DB para Analysis Services, OLE DB para minería de datos o XMLA. Para más información, vea [Conjuntos de filas de esquema de Analysis Services](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets).<br /><br /> La lista siguiente describe varios enfoques para utilizar lconjuntos de filas de esquema:<br /><br /> Ejecute consultas DMV en SQL Server Management Studio o en informes personalizados para acceder a conjuntos de filas de esquema mediante sintaxis SQL. Para obtener más información, vea [Usar vistas de administración dinámica &#40;DMVs&#41; para supervisar Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).<br /><br /> Escriba código ADOMD.NET que llame a un conjunto de filas de esquema.<br /><br /> Ejecute directamente el método XMLA `Discover` contra una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para recuperar la información del conjunto de filas de esquema. Para obtener más información, vea [Método Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover).|  
|XMLA|XMLA es la API de nivel más bajo disponible para un programador de Analysis Services, y es el denominador común que subyace a todas las metodologías de acceso a datos de Analysis Services. XMLA es un estándar del sector, protocolo XML basado en SOAP que admite el acceso universal a los datos de cualquier origen de datos multidimensionales disponible en una conexión HTTP. Utiliza SOAP para formular solicitudes y respuestas para datos multidimensionales. Si la aplicación se ejecuta en una plataforma que no es Windows, se puede usar XMLA para acceder a una base de datos multidimensional que se esté ejecutando en un servidor Windows en la red. Para obtener más información, vea [Desarrollar con XMLA en Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).|  
|Analysis Services Scripting Language (ASSL)|ASSL es un término descriptivo que se aplica a extensiones de Analysis Services del protocolo XMLA. Las extensiones de ASSL permiten que Analysis Services utilice construcciones XMLA más allá de las disposiciones básicas de protocolo, agregando definición de datos, manipulación de datos y soporte de control de datos.  Mientras que los métodos Execute y Discover se describen en el protocolo XMLA, ASSL agrega la funcionalidad siguiente:<br /><br /> Script XMLA<br /><br /> Definiciones de objetos XMLA<br /><br /> Comandos XMLA<br /><br /> <br /><br /> Para obtener más información, vea [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).|  
  
## <a name="see-also"></a>Vea también  
 [Conectar a Analysis Services](../../instances/connect-to-analysis-services.md)   
 [Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desarrollar con XMLA en Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Acceso a datos de modelos tabulares](../../tabular-models/tabular-model-data-access.md)  
  
  
