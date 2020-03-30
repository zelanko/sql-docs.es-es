---
title: SqlDependency en una aplicación ASP.NET
description: Muestra cómo usar notificaciones de consulta desde una aplicación de ASP.NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 8e159a6db1820169cd81caa05e70765ac32f0d56
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896225"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency en una aplicación ASP.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

En el ejemplo de esta sección se muestra cómo usar <xref:Microsoft.Data.SqlClient.SqlDependency> indirectamente aprovechando el objeto <xref:System.Web.Caching.SqlCacheDependency> de ASP.NET. El objeto <xref:System.Web.Caching.SqlCacheDependency> usa <xref:Microsoft.Data.SqlClient.SqlDependency> para escuchar notificaciones y actualizar correctamente la memoria caché.  
  
> [!NOTE]
>  En el ejemplo de código se parte de que las notificaciones de consulta están habilitadas mediante la ejecución de los scripts en [Habilitación de notificaciones de consultas](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Información acerca de la aplicación de ejemplo  
La aplicación de ejemplo usa una única página web de ASP.NET para mostrar información de producto de la base de datos **AdventureWorks** de SQL Server en un control <xref:System.Web.UI.WebControls.GridView>. Cuando se carga la página, el código escribe la hora actual en un control de <xref:System.Web.UI.WebControls.Label>. A continuación, define un objeto de <xref:System.Web.Caching.SqlCacheDependency> y establece propiedades en el objeto <xref:System.Web.Caching.Cache> para almacenar los datos de la memoria caché durante un máximo de tres minutos. Después, el código se conecta a la base de datos y recupera los datos. Cuando se carga la página y la aplicación se ejecuta, ASP.NET recuperará los datos de la memoria caché, lo cual se puede comprobar observando que la hora de la página no cambia. Si los datos que se supervisan cambian, ASP.NET invalida la memoria caché y vuelve a rellenar el control `GridView` con datos nuevos, actualizando la hora que se muestra en el control `Label`.  
  
## <a name="creating-the-sample-application"></a>Creación de la aplicación de ejemplo  
Siga estos pasos para crear y ejecutar la aplicación de ejemplo:  
  
1. Cree un nuevo sitio web de ASP.NET.  
  
2. Agregue un control <xref:System.Web.UI.WebControls.Label> y <xref:System.Web.UI.WebControls.GridView> a la página Default.aspx.  
  
3. Abra el módulo de clase de la página y agregue las siguientes directivas:  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Agregue el siguiente código en el evento `Page_Load` de la página:  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Agregue dos métodos del asistente, `GetConnectionString` y `GetSQL`. La cadena de conexión definida usa seguridad integrada. Debe comprobar que la cuenta que usa dispone de los permisos de base de datos necesarios y que la base de datos de ejemplo, **AdventureWorks**, tiene habilitadas las notificaciones.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Prueba de la aplicación  
La aplicación almacena en caché los datos que se muestran en el formulario web y los actualiza cada tres minutos si no hay ninguna actividad. Si se produce un cambio en la base de datos, la caché se actualiza inmediatamente. Ejecute la aplicación desde Visual Studio, que carga la página en el explorador. La hora de actualización de la caché que se muestra indica cuándo se actualizó la memoria caché por última vez. Espere tres minutos y, a continuación, actualice la página, lo que hará que se produzca un evento de postback. Observe que la hora que se muestra en la página ha cambiado. Si actualiza la página en menos de tres minutos, la hora que se muestra en la página seguirá siendo la misma.  
  
Ahora, actualice los datos de la base de datos mediante un comando UPDATE de Transact-SQL y actualice la página. La hora que se muestra ahora indica que la memoria caché se ha actualizado con los nuevos datos de la base de datos. Tenga en cuenta que aunque la memoria caché se actualiza, la hora que se muestra en la página no cambia hasta que se produce un evento de postback.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Notificaciones de consulta en SQL Server](query-notifications-sql-server.md)
