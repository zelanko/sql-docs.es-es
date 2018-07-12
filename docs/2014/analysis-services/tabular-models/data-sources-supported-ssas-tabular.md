---
title: Orígenes de datos compatibles (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b8aac369dd82f75f251df1195ac29c8ccf3b983
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185302"
---
# <a name="data-sources-supported-ssas-tabular"></a>Orígenes de datos compatibles (SSAS tabular)
  En este tema se describen los tipos de orígenes de datos que se pueden usar con los modelos tabulares.  
  
 Este artículo contiene las secciones siguientes:  
  
-   [Orígenes de datos compatibles](#bkmk_supported_ds)  
  
-   [Orígenes no compatibles](#bkmk_unsupported_ds)  
  
-   [Sugerencias para elegir los orígenes de datos](#bkmk_tips)  
  
##  <a name="bkmk_supported_ds"></a> Orígenes de datos compatibles  
 Puede importar datos de los siguientes orígenes de datos en la tabla siguiente. Al instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el programa de instalación no instala los proveedores enumerados para cada origen de datos. Algunos proveedores ya podrían estar instalados con otras aplicaciones en el equipo; en otros casos tendrá que descargar e instalar el proveedor.  
  
|||||  
|-|-|-|-|  
|Source|Versiones|Tipo de archivo|Proveedores <sup>1</sup>|  
|Bases de datos de Access|Microsoft Access 2003, 2007, 2010.|.accdb o .mdb|Proveedor OLE DB de ACE 14|  
|Bases de datos relacionales de SQL Server|Microsoft SQL Server 2005, 2008, 2008 R2; SQL Server 2012, Microsoft SQL Azure Database <sup>2</sup>|(no aplicable)|Proveedor OLE DB para SQL Server<br /><br /> Proveedor OLE DB de SQL Server Native Client<br /><br /> Proveedor OLE DB de SQL Server Native Client 10.0<br /><br /> Proveedor de datos de .NET Framework para SQL Client|  
|Almacenamiento de datos paralelos de SQL Server (PDW) <sup>3</sup>|2008 R2|(no aplicable)|Proveedor OLE DB para SQL Server PDW|  
|Bases de datos relacionales de Oracle|Oracle 9i, 10g, 11g.|(no aplicable)|Proveedor OLE DB de Oracle<br /><br /> Proveedor de datos de .NET Framework para cliente de Oracle<br /><br /> Proveedor de datos de .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bases de datos relacionales de Teradata|Teradata V2R6, V12|(no aplicable)|Proveedor OLE DB TDOLEDB<br /><br /> Proveedor de datos .NET para Teradata|  
|Bases de datos relacionales de Informix||(no aplicable)|Proveedor OLE DB de Informix|  
|Bases de datos relacionales de IBM DB2|8.1|(no aplicable)|DB2OLEDB|  
|Bases de datos relacionales de Sybase Adaptive Server Enterprise (ASE)|15.0.2|(no aplicable)|Proveedor OLE DB de Sybase|  
|Otras bases de datos relacionales|(no aplicable)|(no aplicable)|Proveedor OLE DB o controlador ODBC|  
|Archivos de texto|(no aplicable)|.txt, .tab, .csv|Proveedor OLE DB ACE 14 para Microsoft Access|  
|Archivos de Microsoft Excel|Excel 97-2003, 2007, 2010|.xlsx, xlsm, .xlsb, .xltx, .xltm|Proveedor OLE DB de ACE 14|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro|Microsoft SQL Server 2008 R2 Analysis Services|.xlsx, xlsm, .xlsb, .xltx, .xltm|ASOLEDB 10.5<br /><br /> (solo se usa con libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se publican en granjas de servidores de SharePoint que tienen instalado [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] )|  
|Cubo de Analysis Services|Microsoft SQL Server 2005, 2008, 2008 R2 Analysis Services|(no aplicable)|ASOLEDB 10|  
|Fuentes de distribución de datos<br /><br /> (se usa para importar datos de informes de Reporting Services, documentos de servicio de Atom, Microsoft Azure Marketplace DataMarket y fuentes de distribución de datos únicas)|Formato Atom 1.0<br /><br /> Cualquier base de datos o documento que se exponen como servicio de datos de Windows Communication Foundation (WCF) (antes ADO.NET Data Services).|.atomsvc para un documento de servicio que define una o más fuentes<br /><br /> .atom para un documento de fuente web de Atom|Proveedor de fuentes de distribución de datos de Microsoft para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> Proveedor de datos de fuentes de distribución de datos de .NET Framework para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Archivos de Office Database Connection||.odc||  
  
 <sup>1</sup> también puede usar el proveedor OLE DB para ODBC.  
  
 <sup>2</sup> para obtener más información acerca de SQL Azure, consulte el sitio web [SQL Azure](http://go.microsoft.com/fwlink/?LinkID=157856).  
  
 <sup>3</sup> para obtener más información acerca de SQL Server PDW, vea el sitio web [almacenamiento de datos paralelos de SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> en algunos casos, mediante el proveedor OLE DB MSDAORA puede producir errores de conexión, especialmente con las versiones más recientes de Oracle. Si encuentra cualquier error, le recomendamos que use otro de los proveedores enumerados para Oracle.  
  
##  <a name="bkmk_unsupported_ds"></a> Orígenes no compatibles  
 El siguiente origen de datos no se admite actualmente:  
  
-   Los documentos de servidor, como bases de datos de Access que ya se han publicado en SharePoint, no se pueden importar.  
  
##  <a name="bkmk_tips"></a> Sugerencias para elegir los orígenes de datos  
  
1.  La importación de tablas desde bases de datos relacionales ahorra trabajo porque durante la importación se usan relaciones de *clave externa* para crear relaciones entre las tablas en el Diseñador de modelos.  
  
2.  La importación de varias tablas y la eliminación posterior de las que no necesite también ahorra trabajo. Si importa tablas de una en una, aún será necesario crear manualmente las relaciones entre las tablas.  
  
3.  Las columnas que contienen datos similares en orígenes de datos diferentes son la base de la creación de relaciones dentro del Diseñador de modelos. Cuando use orígenes de datos heterogéneos, elija tablas con columnas que se puedan asignar a tablas de otros orígenes de datos que contengan datos idénticos o similares.  
  
4.  En ocasiones, los proveedores OLE DB pueden proporcionar un rendimiento más rápido para datos de mayor escala. Cuando deba elegir entre diferentes proveedores para el mismo origen de datos, pruebe en primer lugar el proveedor OLE DB.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos &#40;Tabular de SSAS&#41;](../data-sources-ssas-tabular.md)   
 [Importar datos &#40;Tabular de SSAS&#41;](../import-data-ssas-tabular.md)  
  
  
