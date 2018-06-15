---
title: Admite orígenes de datos (SSAS - Multidimensional) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 907e6cc6deaa9617a4af93ab2080bfe495dacd0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025382"
---
# <a name="supported-data-sources-ssas---multidimensional"></a>Orígenes de datos admitidos (SSAS - Multidimensionales)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En este tema se describen los tipos de orígenes de datos que puede usar en un modelo multidimensional.  
  
##  <a name="bkmk_supported_ds"></a> Orígenes de datos compatibles  
 Puede recuperar datos de los siguientes orígenes de datos en la tabla siguiente. Al instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el programa de instalación no instala los proveedores enumerados para cada origen de datos. Algunos proveedores ya podrían estar instalados con otras aplicaciones en el equipo; en otros casos tendrá que descargar e instalar el proveedor.  
  
> [!NOTE]  
>  También se pueden usar proveedores de otros fabricantes, como el proveedor OLE DB de Oracle, para conectar con bases de datos de otros fabricantes, con la compatibilidad que estos proporcionan.  
  
|||||  
|-|-|-|-|  
|Origen|Versiones|Tipo de archivo|Proveedores*|  
|Bases de datos de Access|Microsoft Access 2010, 2013, 2016|.accdb o .mdb|Proveedor Microsoft Jet 4.0 OLE DB|  
|Bases de datos relacionales de SQL Server*|Microsoft SQL Server 2008, 2008 R2, 2012, 2014, 2016, [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)], almacenamiento de datos SQL Azure, Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> Nota: Para obtener más información acerca de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , consulte [Azure.com](http://go.microsoft.com/fwlink/?LinkID=157856).<br /><br /> Nota: Analytics Platform System (APS) anteriormente se conocía como almacén de datos paralelos de SQL Server (PDW). Originalmente, conectar con PDW desde Analysis Services requería un proveedor de datos especial. Este proveedor se ha sustituido en SQL Server 2012. A partir de SQL Server 2012, el cliente nativo de SQL Server se utiliza para conexiones con PDW y APS. Para obtener más información sobre APS, vea el sitio web [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx).|(no aplicable)|Proveedor OLE DB para SQL Server<br /><br /> Proveedor OLE DB de SQL Server Native Client<br /><br /> Proveedor OLE DB de SQL Server 11.0 Native Client<br /><br /> Proveedor de datos de .NET Framework para SQL Client|  
|Bases de datos relacionales de Oracle|Oracle 9i, 10g, 11g, 12g|(no aplicable)|Proveedor OLE DB de Oracle<br /><br /> Proveedor de datos de .NET Framework para cliente de Oracle<br /><br /> Proveedor de datos de .NET Framework para SQL Server<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bases de datos relacionales de Teradata|Teradata V2R6, V12|(no aplicable)|Proveedor OLE DB TDOLEDB<br /><br /> Proveedor de datos .NET para Teradata|  
|Bases de datos relacionales de Informix|V11.10|(no aplicable)|Proveedor OLE DB de Informix|  
|Bases de datos relacionales de IBM DB2|8.1|(no aplicable)|DB2OLEDB|  
|Bases de datos relacionales de Sybase Adaptive Server Enterprise (ASE)|15.0.2|(no aplicable)|Proveedor OLE DB de Sybase|  
|Otras bases de datos relacionales|(no aplicable)|(no aplicable)|Un proveedor OLE DB|  
  
 \* Los orígenes de datos ODBC no se admiten en soluciones multidimensionales. Aunque Analysis Services por sí mismo controla la conexión, los diseñadores de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] usados para crear soluciones no pueden conectarse a un origen de datos ODBC, ni siquiera cuando usan el controlador MSDASQL. Si los requisitos empresariales incluyen un origen de datos ODBC, considere crear una solución tabular en su lugar.  
  
 ** Algunas características requieren una base de datos relacional de SQL Server que se ejecute localmente. De manera específica, el almacenamiento ROLAP y la reescritura requieren que el origen de datos subyacente sea una base de datos relacional de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Orígenes de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
