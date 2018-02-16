---
title: Las clases fundamentales de AMO | Documentos de Microsoft
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data sources [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
- AMO, data sources
- Analysis Management Objects, data sources
ms.assetid: 440e9287-53a2-4db3-9481-1d2ceb6e5b5a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd2d58e6791a7dd576523f3400264e538ac01307
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="amo-fundamental-classes"></a>Clases fundamentales de AMO
  Las clases fundamentales son el punto inicial cuando se trabaja con AMO (Objetos de administración de análisis). A través de estas clases puede establecer su entorno para el resto de los objetos que se usarán en su aplicación. Las clases fundamentales incluyen los objetos siguientes: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>y <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
 La ilustración siguiente muestra la relación de las clases que se explican en este tema.  
  
 ![Las clases fundamentales de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-fundamentalclasses.gif "clases fundamentales de AMO")  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos de servidor](#ServerObjects)  
  
-   [Objetos de base de datos](#DatabaseObjects)  
  
-   [Objetos DataSource y DataSourceView](#DSandDSV)  
  
##  <a name="ServerObjects"></a> Objetos de servidor  
 Además, obtendrá acceso a los métodos siguientes:  
  
-   Administración de conexiones: Connect, Disconnect, Reconnect y GetConnectionState.  
  
-   Administración de transacciones: BeginTransaction, CommitTransaction y RollbackTransaction.  
  
-   Copia de seguridad y restauración.  
  
-   Ejecución DDL: Execute, CancelCommand, SendXmlaRequest, StartXmlaRequest.  
  
-   Administración de metadatos: UpdateObjects y Validate.  
  
 Para conectar a un servidor, se necesita una cadena de conexión estándar, tal y como se utiliza en ADOMD.NET y OLEDB. Para obtener más información, consulte <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>. El nombre del servidor se puede especificar como una cadena de conexión sin tener que usar un formato de la cadena de conexión.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Server> en <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DatabaseObjects"></a> Objetos de base de datos  
 Para trabajar con un objeto <xref:Microsoft.AnalysisServices.Database> en su aplicación, debe recibir una instancia de la base de datos de la colección de bases de datos del servidor principal. Para crear una base de datos, agregue un objeto <xref:Microsoft.AnalysisServices.Database> a una colección de bases de datos servidor y actualice la nueva instancia en el servidor. Para eliminar una base de datos, quite el objeto <xref:Microsoft.AnalysisServices.Database> utilizando su propio método Drop.  
  
 Se pueden realizar copias de seguridad de las bases de datos mediante el método BackUp (del objeto <xref:Microsoft.AnalysisServices.Database> o del objeto <xref:Microsoft.AnalysisServices.Server> ), pero únicamente se pueden restaurar del objeto <xref:Microsoft.AnalysisServices.Server> con el método Restore.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Database> en <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DSandDSV">Objetos DataSource y DataSourceView</a>  
 Los orígenes de datos se administran mediante <xref:Microsoft.AnalysisServices.DataSourceCollection> de la clase de base de datos. Se puede crear una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Add de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>. Se puede eliminar una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Remove de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>.  
  
 Los objetos <xref:Microsoft.AnalysisServices.DataSourceView> se administran desde el objeto <xref:Microsoft.AnalysisServices.DataSourceViewCollection> en la clase de base de datos.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.DataSource> y <xref:Microsoft.AnalysisServices.DataSourceView> en <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programar objetos fundamentales de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
