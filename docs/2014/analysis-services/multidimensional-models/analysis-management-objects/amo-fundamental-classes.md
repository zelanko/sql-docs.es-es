---
title: Clases fundamentales de AMO | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
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
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55c1b94f30b21b71a6290e7b782e2eeb411d14f5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270031"
---
# <a name="amo-fundamental-classes"></a>Clases fundamentales de AMO
  Las clases fundamentales son el punto inicial cuando se trabaja con AMO (Objetos de administración de análisis). A través de estas clases puede establecer su entorno para el resto de los objetos que se usarán en su aplicación. Las clases fundamentales incluyen los objetos siguientes: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>y <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
 La ilustración siguiente muestra la relación de las clases que se explican en este tema.  
  
 ![Clases fundamentales de AMO](../../../analysis-services/dev-guide/media/amo-fundamentalclasses.gif "clases fundamentales de AMO")  
  
  
  
##  <a name="ServerObjects"></a> Objetos de servidor  
 Además, obtendrá acceso a los métodos siguientes:  
  
-   Administración de conexiones: Connect, Disconnect, Reconnect y GetConnectionState.  
  
-   Administración de transacciones: BeginTransaction, CommitTransaction y RollbackTransaction.  
  
-   Copia de seguridad y restauración.  
  
-   Ejecución DDL: Execute, CancelCommand, SendXmlaRequest, StartXmlaRequest.  
  
-   Administración de metadatos: UpdateObjects y Validate.  
  
 Para conectar a un servidor, se necesita una cadena de conexión estándar, tal y como se utiliza en ADOMD.NET y OLEDB. Para obtener más información, consulta <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>. El nombre del servidor se puede especificar como una cadena de conexión sin tener que usar un formato de la cadena de conexión.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Server> en <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DatabaseObjects"></a> Objetos de base de datos  
 Para trabajar con un objeto <xref:Microsoft.AnalysisServices.Database> en su aplicación, debe recibir una instancia de la base de datos de la colección de bases de datos del servidor principal. Para crear una base de datos, agregue un objeto <xref:Microsoft.AnalysisServices.Database> a una colección de bases de datos servidor y actualice la nueva instancia en el servidor. Para eliminar una base de datos, quite el objeto <xref:Microsoft.AnalysisServices.Database> utilizando su propio método Drop.  
  
 Se pueden realizar copias de seguridad de las bases de datos mediante el método BackUp (del objeto <xref:Microsoft.AnalysisServices.Database> o del objeto <xref:Microsoft.AnalysisServices.Server> ), pero únicamente se pueden restaurar del objeto <xref:Microsoft.AnalysisServices.Server> con el método Restore.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Database> en <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DSandDSV"></a> Objetos DataSource y DataSourceView  
 Los orígenes de datos se administran mediante <xref:Microsoft.AnalysisServices.DataSourceCollection> de la clase de base de datos. Se puede crear una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Add de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>. Se puede eliminar una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Remove de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>.  
  
 Los objetos <xref:Microsoft.AnalysisServices.DataSourceView> se administran desde el objeto <xref:Microsoft.AnalysisServices.DataSourceViewCollection> en la clase de base de datos.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.DataSource> y <xref:Microsoft.AnalysisServices.DataSourceView> en <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](amo-classes-introduction.md)   
 [Programar objetos fundamentales de AMO](programming-amo-fundamental-objects.md)  
  
  
