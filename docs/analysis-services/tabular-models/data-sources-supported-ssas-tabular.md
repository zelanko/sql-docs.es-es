---
title: Orígenes de datos admitidos en los modelos tabulares de 1200 de SQL Server Analysis Services | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31ef1eb37f85e3e9ec7a7ea7d7eadee03b6c9c20
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>Orígenes de datos admiten en SQL Server Analysis Services modelos tabulares 1200
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
Este artículo describen los tipos de orígenes de datos que pueden utilizarse con modelos tabulares de SQL Server Analysis Services en 1200 y nivel de compatibilidad inferior. 

Para los modelos en los niveles de compatibilidad de 1400, consulte [orígenes de datos admitidos en los modelos de 1400 tabulares de SQL Server Analysis Services](data-sources-supported-ssas-tabular-1400.md).

Para los servicios de análisis de Azure, consulte [orígenes de datos admitidos en Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource).
  
##  <a name="bkmk_supported_ds"></a> Orígenes de datos admitidos para los modelos tabulares en memoria  
Al instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el programa de instalación no instala los proveedores enumerados para cada origen de datos. Algunos proveedores podrían estar instalados con otras aplicaciones en el equipo. En otros casos, debe descargar e instalar al proveedor.  
  
|||||  
|-|-|-|-|  
|Origen|Versiones|Tipo de archivo|Proveedores|  
|Bases de datos de Access|Microsoft Access 2010 y versiones posteriores.|.accdb o .mdb|Proveedor OLE DB de ACE 14|  
|Bases de datos relacionales de SQL Server|SQL Server 2008 y versiones posterior, almacenamiento de datos de SQL Server 2008 y versiones posterior, Azure base de datos SQL, almacenamiento de datos de SQL Azure, Analytics Platform System (APS)<br /><br /> <br /><br /> Analytics Platform System (APS) anteriormente se conocía como almacén de datos paralelos de SQL Server (PDW). Originalmente, conectar con PDW desde Analysis Services requería un proveedor de datos especial. Este proveedor se ha sustituido en SQL Server 2012. A partir de SQL Server 2012, el cliente nativo de SQL Server se utiliza para conexiones con PDW y APS. |(no aplicable)|Proveedor OLE DB para SQL Server<br /><br /> Proveedor OLE DB de SQL Server Native Client<br /><br /> Proveedor OLE DB de SQL Server Native Client 10.0<br /><br /> Proveedor de datos de .NET Framework para SQL Client|  
|Bases de datos relacionales de Oracle|Oracle 9i y versiones posteriores.|(no aplicable)|Proveedor OLE DB de Oracle<br /><br /> Proveedor de datos de .NET Framework para cliente de Oracle<br /><br /> Proveedor de datos de .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bases de datos relacionales de Teradata|Teradata V2R6 y versiones posteriores|(no aplicable)|Proveedor OLE DB TDOLEDB<br /><br /> Proveedor de datos .NET para Teradata|  
|Bases de datos relacionales de Informix||(no aplicable)|Proveedor OLE DB de Informix|  
|Bases de datos relacionales de IBM DB2|8.1|(no aplicable)|DB2OLEDB|  
|Bases de datos relacionales de Sybase Adaptive Server Enterprise (ASE)|15.0.2|(no aplicable)|Proveedor OLE DB de Sybase|  
|Otras bases de datos relacionales|(no aplicable)|(no aplicable)|Proveedor OLE DB o controlador ODBC|  
|Archivos de texto|(no aplicable)|.txt, .tab, .csv|Proveedor OLE DB ACE 14 para Microsoft Access|  
|Archivos de Microsoft Excel|Excel 2010 y versiones posteriores|.xlsx, xlsm, .xlsb, .xltx, .xltm|Proveedor OLE DB de ACE 14|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro|Microsoft SQL Server 2008 y versiones posteriores de Analysis Services|.xlsx, xlsm, .xlsb, .xltx, .xltm|ASOLEDB 10.5<br /><br /> (solo se usa con libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se publican en granjas de servidores de SharePoint que tienen instalado [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] )|  
|Cubo de Analysis Services|Microsoft SQL Server 2008 y versiones posteriores de Analysis Services|(no aplicable)|ASOLEDB 10|  
|Fuentes de distribución de datos<br /><br /> (se usa para importar datos de informes de Reporting Services, documentos de servicio de Atom, Microsoft Azure Marketplace DataMarket y fuentes de distribución de datos únicas)|Formato Atom 1.0<br /><br /> Cualquier base de datos o documento que se exponen como servicio de datos de Windows Communication Foundation (WCF) (antes ADO.NET Data Services).|`.atomsvc` para un documento de servicio que define una o más fuentes<br /><br /> .atom para un documento de fuente web de Atom|Proveedor de fuentes de distribución de datos de Microsoft para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Proveedor de datos de fuentes de distribución de datos de .NET Framework para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Archivos de Office Database Connection||.odc||  
  
  
##  <a name="bkmk_supported_ds_dq"></a> Orígenes de datos admitidos para los modelos DirectQuery  
 DirectQuery es una alternativa al modo de almacenamiento en memoria, que enruta consultas a sistemas de datos de back-end y devuelve los resultados directamente desde dichos sistemas en lugar de almacenar todos los datos dentro del modelo (y en memoria RAM una vez cargado el modelo). Dado que Analysis Services tiene que formular consultas en la sintaxis de consulta de base de datos nativa, se admite un subconjunto más pequeño de orígenes de datos para este modo.  
  
Origen de datos   |Versiones  |Proveedores
---------|---------|---------
Microsoft SQL Server    |  2008 y versiones posteriores      |       Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para el cliente SQL  
Base de datos SQL de Microsoft Azure    |   Todos      |  Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para el cliente SQL            
Almacenamiento de datos de Microsoft Azure SQL     |   Todos     |  Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para el cliente SQL       
Microsoft SQL Analytics Platform System (APS)     |   Todos      |  Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para el cliente SQL       
Bases de datos relacionales de Oracle     |  Oracle 9i y versiones posteriores       |  Proveedor OLE DB de Oracle       
Bases de datos relacionales de Teradata    |  Teradata V2R6 y versiones posteriores     | Proveedor de datos .NET para Teradata    

  
##  <a name="bkmk_tips"></a> Sugerencias para elegir los orígenes de datos  
  
La importación de tablas desde bases de datos relacionales ahorra trabajo porque durante la importación se usan relaciones de *clave externa* para crear relaciones entre las tablas en el Diseñador de modelos.  
  
La importación de varias tablas y la eliminación posterior de las que no necesite también ahorra trabajo. Si importa tablas de una en una, aún será necesario crear manualmente las relaciones entre las tablas.  
  
Las columnas que contienen datos similares en orígenes de datos diferentes son la base de la creación de relaciones dentro del Diseñador de modelos. Cuando use orígenes de datos heterogéneos, elija tablas con columnas que se puedan asignar a tablas de otros orígenes de datos que contengan datos idénticos o similares.  
  
Proveedores OLE DB en ocasiones, pueden proporcionar un rendimiento más rápido para los datos a gran escala. Cuando deba elegir entre diferentes proveedores para el mismo origen de datos, pruebe en primer lugar el proveedor OLE DB.  

## <a name="see-also"></a>Vea también

[Orígenes de datos admiten en SQL Server Analysis Services 1400 los modelos tabulares](data-sources-supported-ssas-tabular-1400.md)

[Orígenes de datos admitidos en los servicios de análisis de Azure](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   