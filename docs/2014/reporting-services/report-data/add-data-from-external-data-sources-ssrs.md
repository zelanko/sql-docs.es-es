---
title: Agregar datos de orígenes de datos externos (SSRS)
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/27/2017
ms.openlocfilehash: 54358529577061ad99c634fa6cc4ce9d98792e0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67412680"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>Agregar datos de orígenes de datos externos (SSRS)

Para recuperar datos de un origen de datos externo, use una conexión de datos. La información de la conexión de datos la suele proporcionar el propietario del origen de datos externo, que es responsable de otorgar los permisos y de especificar qué tipos de credenciales se han de usar. La información de la conexión de datos se guarda como un origen de datos de informe. El tipo de origen de datos especifica qué extensión de datos usar para recuperar los datos.  

##  <a name="understanding-data-access-technology"></a><a name="DataAccess"></a>Descripción de la tecnología de acceso a datos  

Recuperar los datos para un conjunto de datos de informe requiere varios niveles de software de acceso a datos. La siguiente lista proporciona una descripción simple de cómo funcionan los informes con las tecnologías de acceso a datos:  

-   **Aplicación e interfaz de usuario:** la aplicación Generador de informes que utiliza para crear un origen de datos, agregar una referencia a un origen de datos compartido, agregar un conjunto de datos compartido o agregar un elemento de informe que incluya los orígenes de datos y conjuntos de datos de los que depende.  

-   **Elementos de la definición de informe:** los conjuntos de datos y orígenes de datos forman parte de la definición del informe. Una vez publicado un informe en un servidor de informes, los orígenes de datos compartidos y los conjuntos de datos compartidos se administran con independencia desde la definición de informe.  

  -   **Origen de datos y origen de datos compartidos:** el elemento de una definición de informe que incluye la información sobre el tipo de extensión de procesamiento de datos, la información de conexión y la autenticación.  

  -   **Colección de campos y conjuntos de datos:** elemento de una definición de informe que incluye la consulta, la colección de campos y los tipos de datos de campo.  

-   **Extensiones de datos de Reporting Services:** extensiones de datos integrados que se instalan con el Generador de informes. Una extensión de datos proporciona una funcionalidad que controla los parámetros de autenticación, agregados de servidor y parámetros de varios valores.  

-   **Proveedor de datos:** el software que administra la conexión y recuperación de datos desde el origen de datos externo. El proveedor de datos define la sintaxis de la cadena de conexión. La mayoría de las extensiones de datos se compilan sobre una capa del proveedor de datos.  

-   **Origen de datos externo:** de dónde recuperar los datos de informe; por ejemplo, una base de datos, un archivo, un cubo o un servicio web.  

> [!NOTE]  
>  Al no estar conectado a un servidor de informes, puede elegir desde las extensiones de datos que se instalan con el Generador de informes. Obtiene acceso a los datos como un usuario único utilizando las credenciales de su equipo. Al estar conectado a un servidor de informes, puede elegir desde las extensiones de datos que se instalan en el servidor de informes. Obtiene acceso a los datos como uno de los diferentes usuarios que ejecutan el informe, para lo que utiliza las credenciales del servidor de informes. Para más información, vea [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  

##  <a name="understanding-report-data"></a><a name="ReportData"></a> Descripción de los datos de informe  
En su forma más simple, un informe muestra los datos desde un conjunto de datos de informe de una región de datos de la página del informe, es decir, de una tabla única, gráfico, matriz u otro tipo de región de datos del informe. Los datos de un conjunto de datos de informe proceden del primer conjunto de resultados que se devuelve desde un comando de consulta único que ejecuta desde un acceso de solo lectura a un origen de datos externo. Todas las regiones de datos se expanden lo necesario para mostrar todos los datos del conjunto de datos.  

Los datos de un conjunto de datos suelen ser tabulares. Las columnas son los campos de la consulta del conjunto de datos. Las filas proceden de las filas del conjunto de resultados. Puede utilizar los siguientes tipos generalizados de datos en un informe:  

-   Datos rectangulares. Datos de un conjunto de resultados que tiene el mismo número de columnas en cada fila.  

-   Los datos jerárquicos se admiten como un conjunto de filas planas.  

  -   No se admiten jerarquías desiguales, en las que hay un número diferente de columnas en cada fila de datos. Para algunas extensiones de datos, esto tiene algunas implicaciones.  

  -   Las extensiones de datos que funcionan con orígenes de datos multidimensionales usan XML para el protocolo Analysis y recuperan los datos como un conjunto de filas plano, no como un conjunto de celdas.  

  -   La extensión de datos XML aplana automáticamente los datos XML que se van a usar en un informe. Si la primera instancia de un elemento XML no incluye todos los atributos o subelementos, es posible que los datos no estén disponibles como datos de informe.  

-   Se admiten los datos recursivos. Un conjunto de resultados que contiene una jerarquía de datos recursiva incluye toda la información sobre la estructura de jerarquía en un conjunto de resultados rectangular. Por ejemplo, el informe a estructurar en una compañía puede ser representado por una tabla que incluya dos columnas: un empleado y un administrador. Cada administrador también es un empleado con un administrador. El administrador superior normalmente contiene un null o algún otro identificador que indique que este empleado no tiene ningún administrador.  



##  <a name="working-with-data-types"></a><a name="DataTypes"></a>Trabajar con tipos de datos  
Cuando se crea un conjunto de datos, los tipos de datos de los campos se asignan a un subconjunto de tipos de datos de Common Language Runtime (CLR) de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Los tipos de datos que no pueden asignarse claramente se devuelven como cadenas. Para obtener más información sobre cómo trabajar con tipos de datos de campo, vea [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md). Cuando se crea un parámetro, el tipo de datos debe ser un tipo de datos de definición de informe compatible. Para obtener más información sobre cómo asignar tipos de datos del proveedor de datos a un parámetro de informe, vea [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md).  



##  <a name="how-to-topics"></a><a name="HowTo"></a>Temas de procedimientos  
Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  

[Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  

[Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  

[Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

## <a name="in-this-section"></a><a name="InThisSection"></a>En esta sección  

Los siguientes temas proporcionan información sobre cada extensión de datos integrados.  

|Tema|Tipo de origen de datos|  
|-----------|----------------------|  
|[Tipo de conexión de SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[Tipo de conexión de Analysis Services para MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Tipo de conexión de PowerPivot &#40;SSRS&#41;](power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Tipo de conexión de lista de SharePoint &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Lista de SharePoint|  
|[Tipo de conexión SQL Azure &#40;SSRS&#41;](sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[Tipo de conexión Almacenamiento de datos paralelo de SQL Server &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[Tipo de conexión de SAP NetWeaver BI &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Tipo de conexión de Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[Tipo de conexión OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md)|OLE DB|  
|[Tipo de conexión ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md)|ODBC|  
|[Tipo de conexión XML &#40;SSRS&#41;](xml-connection-type-ssrs.md)|XML|  

## <a name="related-sections"></a><a name="Related"></a> Secciones relacionadas  

Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  

|Tema|Descripción|  
|-----------|-----------------|  
|[Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-datasets-ssrs.md)|Proporciona información general sobre cómo obtener acceso a los datos del informe.|  
|[Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)|Proporciona información sobre las conexiones de datos y los orígenes de datos.|  
|[Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|Proporciona información sobre conjuntos de datos compartidos e incrustados.|  
|[Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)|Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.|  
|[Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de .|Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.|  
|[Introducción a las extensiones de procesamiento de datos](../extensions/data-processing/data-processing-extensions-overview.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [de](https://go.microsoft.com/fwlink/?linkid=121312).|Proporciona a los usuarios expertos información detallada sobre las extensiones de datos.|  

## <a name="see-also"></a>Consulte también  

- [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-datasets-ssrs.md)
- [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md)