---
title: Las clases fundamentales de AMO | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffa7973757ce41a3975bcbb70170679109527e42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
##  <a name="DSandDSV"></a> Objetos DataSource y DataSourceView  
 Los orígenes de datos se administran mediante <xref:Microsoft.AnalysisServices.DataSourceCollection> de la clase de base de datos. Se puede crear una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Add de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>. Se puede eliminar una instancia de <xref:Microsoft.AnalysisServices.DataSource> mediante el método Remove de un objeto <xref:Microsoft.AnalysisServices.DataSourceCollection>.  
  
 Los objetos <xref:Microsoft.AnalysisServices.DataSourceView> se administran desde el objeto <xref:Microsoft.AnalysisServices.DataSourceViewCollection> en la clase de base de datos.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.DataSource> y <xref:Microsoft.AnalysisServices.DataSourceView> en <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programar objetos fundamentales de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
