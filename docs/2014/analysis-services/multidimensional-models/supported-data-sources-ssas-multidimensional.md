---
title: Orígenes de datos compatibles (SSAS Multidimensional) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
caps.latest.revision: 59
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 130e0e904dcd60b8dc7838cfc8e57f7589739857
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200825"
---
# <a name="data-sources-supported-ssas-multidimensional"></a>Orígenes de datos compatibles (SSAS Multidimensional)
  En este tema se describen los tipos de orígenes de datos que puede usar en un modelo multidimensional.  
  
##  <a name="bkmk_supported_ds"></a> Orígenes de datos compatibles  
 Puede recuperar datos de los siguientes orígenes de datos en la tabla siguiente. Al instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el programa de instalación no instala los proveedores enumerados para cada origen de datos. Algunos proveedores ya podrían estar instalados con otras aplicaciones en el equipo; en otros casos tendrá que descargar e instalar el proveedor.  
  
> [!NOTE]  
>  También se pueden usar proveedores de otros fabricantes, como el proveedor OLE DB de Oracle, para conectar con bases de datos de otros fabricantes, con la compatibilidad que estos proporcionan.  
  
|||||  
|-|-|-|-|  
|Source|Versiones|Tipo de archivo|Proveedores de <sup>1</sup>|  
|Bases de datos de Access|Microsoft Access 2007, 2010, 2013.|.accdb o .mdb|Proveedor Microsoft Jet 4.0 OLE DB|  
|Bases de datos relacionales de SQL Server <sup>5</sup>|Microsoft SQL Server 2005, 2008, 2008 R2, 2012, 2014 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>, almacenamiento de datos en paralelo de SQL Server (PDW) <sup>3</sup>|(no aplicable)|Proveedor OLE DB para SQL Server<br /><br /> Proveedor OLE DB de SQL Server Native Client<br /><br /> Proveedor OLE DB de SQL Server 11.0 Native Client<br /><br /> Proveedor de datos de .NET Framework para SQL Client|  
|Bases de datos relacionales de Oracle|Oracle 9i, 10g, 11g.|(no aplicable)|Proveedor OLE DB de Oracle<br /><br /> Proveedor de datos de .NET Framework para cliente de Oracle<br /><br /> Proveedor de datos de .NET Framework para SQL Server<br /><br /> Proveedor OLE DB MSDAORA <sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bases de datos relacionales de Teradata|Teradata V2R6, V12|(no aplicable)|Proveedor OLE DB TDOLEDB<br /><br /> Proveedor de datos .NET para Teradata|  
|Bases de datos relacionales de Informix|V11.10|(no aplicable)|Proveedor OLE DB de Informix|  
|Bases de datos relacionales de IBM DB2|8.1|(no aplicable)|DB2OLEDB|  
|Bases de datos relacionales de Sybase Adaptive Server Enterprise (ASE)|15.0.2|(no aplicable)|Proveedor OLE DB de Sybase|  
|Otras bases de datos relacionales|(no aplicable)|(no aplicable)|Un proveedor OLE DB|  
  
 <sup>1</sup> orígenes de datos ODBC no se admiten en las soluciones multidimensionales. Aunque Analysis Services por sí mismo controla la conexión, los diseñadores de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] usados para crear soluciones no pueden conectarse a un origen de datos ODBC, ni siquiera cuando usan el controlador MSDASQL. Si los requisitos empresariales incluyen un origen de datos ODBC, considere crear una solución tabular en su lugar.  
  
 <sup>2</sup> para obtener más información, consulte [!INCLUDE[ssSDS](../../includes/sssds-md.md)], en [azure.microsoft.com](http://go.microsoft.com/fwlink/?LinkID=157856).  
  
 <sup>3</sup> para obtener más información acerca de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] PDW, vea [almacenamiento de datos paralelos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> en algunos casos, mediante el proveedor OLE DB MSDAORA puede producir errores de conexión, particularmente con versiones más recientes de Oracle. Si encuentra cualquier error, le recomendamos que use otro de los proveedores enumerados para Oracle.  
  
 <sup>5</sup> algunas características requieren una base de datos relacional de SQL Server se ejecuta en local. De manera específica, el almacenamiento de reescritura y el almacenamiento ROLAP requieren que el origen de datos subyacente sea una base de datos relacional de SQL Server  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos &#40;SSAS Tabular&#41;](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [Orígenes de datos en modelos multidimensionales](data-sources-in-multidimensional-models.md)   
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)  
  
  