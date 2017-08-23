---
title: Datos de destino de Streaming | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e95b4d887bea5783be935a40877d590b8e8dcff
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="data-streaming-destination"></a>Destino de streaming de datos
  El **Destino de streaming de datos** es un componente de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) que permite que el **proveedor OLE DB para SSIS** consuma la salida de un paquete SSIS como un conjunto de resultados tabular. Para crear un servidor vinculado que utilice el proveedor OLE DB para SSIS y, después, ejecutar una consulta SQL en el servidor vinculado para mostrar los datos devueltos por el paquete SSIS.  
  
 En el ejemplo siguiente, la siguiente consulta devuelve una salida del paquete Package.dtsx en el proyecto SSISPackagePublishing de la carpeta Power BI del catálogo de SSIS. Esta consulta utiliza el servidor vinculado llamado [Default Linked Server for Integration Services] que, a su vez, usa el nuevo proveedor OLE DB para SSIS. En la consulta se incluye el nombre de la carpeta, del proyecto y del paquete del catálogo de SSIS. El proveedor OLE DB para SSIS ejecuta el paquete especificado en la consulta y devuelve el conjunto de resultados tabulares.  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Componentes de publicación de las fuentes de distribución de datos  
 Entre los componentes de publicación de las fuentes de distribución de datos se incluyen los siguientes: el proveedor OLE DB para SSIS, el Destino de streaming de datos y el Asistente para publicación de paquetes SSIS. El asistente permite publicar un paquete SSIS como una vista SQL en una instancia de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El asistente lo ayudará a crear un servidor vinculado que use el proveedor OLE DB para SSIS y una vista SQL que represente una consulta en el servidor vinculado. Puede ejecutar la vista para consultar los resultados del paquete SSIS como un conjunto de datos tabular.  
  
 Para confirmar que está instalado el proveedor SSISOLEDB, en SQL Server Management Studio, expanda **Objetos de servidor**, **Servidores vinculados**y **Proveedores**, y confirme que aparece el proveedor **SSISOLEDB** . Haga doble clic en **SSISOLEDB**, habilite **Permitir InProcess** si no está habilitado y haga clic en **Aceptar**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Publicación de un paquete SSIS como una vista SQL  
 El siguiente procedimiento describe los pasos para publicar un paquete SSIS como una vista SQL.  
  
1.  Crear un paquete SSIS con un componente **Destino de streaming de datos** e implemente el paquete en el catálogo de SSIS.  
  
2.  Abra el **Asistente para publicación de paquetes SSIS** ejecutando ISDataFeedPublishingWizard.exe desde C:\Archivos de programa\Microsoft SQL Server\130\DTS\Binn o el Asistente para publicación de fuentes de distribución de datos de SSIS en el menú Inicio.  
  
     El asistente crea un servidor vinculado mediante el proveedor OLE DB para SSIS (SSISOLEDB) y, tras ello, genera una vista SQL que se compone de una consulta en el servidor vinculado. Esta consulta incluye el nombre de la carpeta, del proyecto y del paquete en el catálogo de SSIS.  
  
3.  Ejecute la vista SQL en SQL Server Management Studio y consulte los resultados del paquete SSIS. La vista envía una consulta al proveedor OLE DB para SSIS mediante el servidor vinculado que ha creado. El proveedor OLE DB para SSIS ejecuta el paquete especificado en la consulta y devuelve el conjunto de resultados tabulares.  
  
> [!IMPORTANT]  
>  Para obtener instrucciones detalladas, vea [Tutorial: Publicar un paquete SSIS como una vista SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>Exposición de datos de salida de un paquete SSIS como una fuente OData mediante el Centro de administración de Power BI  
 Mediante el Centro de administración de Power BI, los administradores de TI pueden exponer datos procedentes de orígenes de datos locales, como fuentes de OData, a los usuarios. El Centro de administración de Power BI, de manera predeterminada, permite registrar solo los orígenes de datos de SQL Server. Pero puede registrar paquetes SSIS como orígenes de datos en el portal mediante **Destino de streaming de datos** y el **proveedor Microsoft OLE DB para SQL Server Integration Services (SSISOLEDB)** , y exponer los datos de resultados del paquete SSIS como una fuente de OData al usuario.  
  
 El Centro de administración permite publicar vistas en una base de datos de SQL Server. Como consecuencia, puede utilizar el Asistente para publicación de paquetes SSIS a fin de publicar un paquete SSIS como una vista SQL. Después, puede seleccionar la vista que se incluirá en la fuente de OData en el Centro de administración de Power BI. Un administrador de datos puede consumir la fuente desde el paquete SSIS mediante el complemento Power Query para Excel.  
  
 Para ver un tutorial detallado, consulte [Publish SSIS Packages as OData Feed Sources](http://go.microsoft.com/fwlink/?LinkID=317367)(Publicación de paquetes SSIS como orígenes de fuentes de OData).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Tutorial: Publicar un paquete SSIS como una vista SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [Configuración del destino de streaming de datos](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## <a name="see-also"></a>Vea también  
 [Publish SSIS Packages as OData Feed Sources](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
