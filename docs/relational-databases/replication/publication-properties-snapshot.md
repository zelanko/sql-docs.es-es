---
title: "Propiedades de la publicaci&#243;n, Instant&#225;nea | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.snapshotformat.f1"
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Propiedades de la publicaci&#243;n, Instant&#225;nea
  La página **Instantánea** del cuadro de diálogo **Propiedades de la publicación** permite establecer el formato de instantánea, la ubicación de la carpeta de instantáneas y los scripts que deben ejecutarse antes y después de aplicar la instantánea. La carpeta de instantáneas debe designarse como recurso compartido y debe disponer de los permisos necesarios para que los agentes puedan leer y escribir archivos en ella. Para obtener más información acerca de cómo proteger la carpeta adecuadamente, consulte [proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  Los cambios requieren una nueva instantánea para la publicación. Para obtener más información, consulte [Propiedades de artículo y publicación de cambio](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## Opciones  
 **Formato de instantánea**  
 Permite seleccionar el modo nativo o el modo de carácter para el formato de instantánea.  
  
-   Seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecutan SQL Server** si todos los suscriptores son instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distinto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. El formato nativo de instantánea ofrece el mejor rendimiento.  
  
-   Seleccione **carácter: necesario si un publicador o suscriptor no ejecuta SQL Server** si hay suscriptores que ejecutan [!INCLUDE[ssEW](../../includes/ssew-md.md)] o no son[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 **Ubicación de archivos de instantánea**  
 Permite seleccionar la ubicación en la que se almacenarán los archivos de instantánea. Pueden almacenarse en la ubicación predeterminada; también pueden almacenarse en una ubicación alternativa (o en la ubicación predeterminada y en una ubicación alternativa). Los archivos almacenados en una ubicación alternativa pueden comprimirse.  
  
-   Seleccione **Poner los archivos en la carpeta predeterminada** para usar la carpeta de instantáneas predeterminada para el publicador. La ubicación de la carpeta de instantáneas es de sólo lectura en este cuadro de diálogo, ya que sólo se puede cambiar para el publicador en la **Propiedades del distribuidor** cuadro de diálogo. Para obtener más información, consulte [especificar la ubicación de instantánea predeterminada & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   Seleccione **Poner los archivos en la siguiente carpeta** para especificar una ubicación alternativa, o adicional, a la ubicación predeterminada. Escriba una ruta en el cuadro de texto o haga clic en **Examinar** para navegar a una ubicación. Seleccione **Comprimir archivos de instantánea en esta carpeta** para comprimir los archivos en la ubicación de instantáneas alternativa. La ubicación alternativa puede estar en otro servidor, en una unidad de red o en un medio extraíble, como un CD-ROM o un disco extraíble. Para obtener más información, consulte [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) y [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
 **Ejecutar scripts adicionales**  
 Permite especificar los scripts que se deben ejecutar antes y después de aplicar la instantánea al suscriptor. Si el **Formato de instantánea** es **Carácter**no se pueden especificar scripts.  
  
 Los scripts son opcionales, pero proporcionan un modo adecuado de ejecutar comandos y aplicar cambios administrativos en los suscriptores. Para obtener más información acerca de cómo ejecutar secuencias de comandos, consulte [Ejecutar Scripts antes y después de aplicar la instantánea](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Escriba una ruta en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script.  
  
-   Escriba una ruta en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script.  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  