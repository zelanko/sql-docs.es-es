---
title: Propiedades de la publicación, Instantánea | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ebf115466a916922444818d11ccd3855c49f825
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214125"
---
# <a name="publication-properties-snapshot"></a>Propiedades de la publicación, Instantánea
  La página **Instantánea** del cuadro de diálogo **Propiedades de la publicación** permite establecer el formato de instantánea, la ubicación de la carpeta de instantáneas y los scripts que deben ejecutarse antes y después de aplicar la instantánea. La carpeta de instantáneas debe designarse como recurso compartido y debe disponer de los permisos necesarios para que los agentes puedan leer y escribir archivos en ella. Para obtener más información sobre cómo proteger la carpeta adecuadamente, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  Los cambios requieren una nueva instantánea para la publicación. Para obtener más información, vea [Cambiar las propiedades de la publicación y de los artículos](publish/change-publication-and-article-properties.md).  
  
## <a name="options"></a>Opciones  
 **Formato de instantánea**  
 Permite seleccionar el modo nativo o el modo de carácter para el formato de instantánea.  
  
-   Seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** si todos los suscriptores son instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no son [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. El formato nativo de instantánea ofrece el mejor rendimiento.  
  
-   Seleccione **Carácter: necesario si un publicador o suscriptor no ejecuta SQL Server** si hay suscriptores que ejecutan [!INCLUDE[ssEW](../../includes/ssew-md.md)] o suscriptores que no son de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Ubicación de archivos de instantánea**  
 Permite seleccionar la ubicación en la que se almacenarán los archivos de instantánea. Pueden almacenarse en la ubicación predeterminada; también pueden almacenarse en una ubicación alternativa (o en la ubicación predeterminada y en una ubicación alternativa). Los archivos almacenados en una ubicación alternativa pueden comprimirse.  
  
-   Seleccione **Poner los archivos en la carpeta predeterminada** para usar la carpeta de instantáneas predeterminada para el publicador. La ubicación de la carpeta de instantáneas se muestra en este cuadro de diálogo como de solo lectura, ya que los permisos del publicador solamente pueden cambiarse en el cuadro de diálogo **Propiedades del distribuidor** . Para obtener más información, vea [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md) (Especificar la ubicación predeterminada de instantáneas (SQL Server Management Studio).  
  
-   Seleccione **Poner los archivos en la siguiente carpeta** para especificar una ubicación alternativa, o adicional, a la ubicación predeterminada. Escriba una ruta en el cuadro de texto o haga clic en **Examinar** para navegar a una ubicación. Seleccione **Comprimir archivos de instantánea en esta carpeta** para comprimir los archivos en la ubicación de instantáneas alternativa. La ubicación alternativa puede estar en otro servidor, en una unidad de red o en un medio extraíble, como un CD-ROM o un disco extraíble. Para obtener más información, consulte [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md) y [Compressed Snapshots](compressed-snapshots.md).  
  
 **Ejecutar scripts adicionales**  
 Permite especificar los scripts que se deben ejecutar antes y después de aplicar la instantánea al suscriptor. Si el **Formato de instantánea** es **Carácter**no se pueden especificar scripts.  
  
 Los scripts son opcionales, pero proporcionan un modo adecuado de ejecutar comandos y aplicar cambios administrativos en los suscriptores. Para obtener más información, vea [Ejecutar scripts antes y después de aplicar la instantánea](execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Escriba una ruta en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script.  
  
-   Escriba una ruta en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** o haga clic en **Examinar** para especificar una ubicación para el script.  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
 [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)   
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)  
  
  
