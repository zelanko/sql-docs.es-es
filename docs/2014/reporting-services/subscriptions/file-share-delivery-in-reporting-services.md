---
title: Entrega a recursos compartidos de archivos en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 72c49b9bb1b7d018f6650b8042e306234fd74caf
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036896"
---
# <a name="file-share-delivery-in-reporting-services"></a>Entrega a recursos compartidos de archivos en Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incorpora una extensión de entrega a recursos compartidos de archivos que permite entregar un informe a una carpeta. Esta extensión está disponible de forma predeterminada y no requiere configuración adicional. Para que la entrega de archivos sea satisfactoria, debe establecer permisos de escritura en la carpeta compartida. Además, los usuarios que necesitan acceso a los informes deben tener permisos de lectura en la carpeta compartida.  
  
 Para distribuir un informe a un recurso compartido de archivos, defina una suscripción estándar o controlada por datos. Puede suscribirse y solicitar la entrega de solo un informe al mismo tiempo. Para información sobre cómo usar la entrega a recursos compartidos en una suscripción controlada por datos, vea [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md). Además, la cuenta que ejecuta las suscripciones a recursos compartidos de archivos remotos necesita derechos para iniciar sesión localmente en el equipo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
 En este tema:  
  
-   [Características de los informes que se entregan a una carpeta compartida](#bkmk_Characteristics)  
  
-   [Carpetas de destino](#bkmk_target_folders)  
  
-   [Formatos de archivo](#bkmk_file_formats)  
  
-   [Opciones de archivo](#bkmk_file_options)  
  
##  <a name="bkmk_Characteristics"></a> Características de los informes que se entregan a una carpeta compartida  
 A diferencia de los informes que se hospedan y administran en un servidor de informes, los informes que se entregan a una carpeta compartida son archivos estáticos. Las características interactivas que se hayan definido para el informe no funcionarán para los informes almacenados como archivos en el sistema de archivos. Las características interactivas aparecen representadas como elementos estáticos. Por ejemplo, si entrega un informe de matriz, el archivo resultante muestra la vista de nivel superior del informe; no se pueden expandir las filas ni las columnas para ver datos complementarios. Si el informe incluye gráficos, se utiliza la presentación predeterminada. Si el informe se vincula a otro informe, el vínculo se representa como texto estático. Si desea conservar las características interactivas de un informe entregado, utilice la entrega por correo electrónico. Para más información, vea [Entrega por correo electrónico en Reporting Services](e-mail-delivery-in-reporting-services.md).  
  
##  <a name="bkmk_target_folders"></a> Carpetas de destino  
 Cuando defina una suscripción que utilice entrega a recursos compartidos de archivos, debe especificar una carpeta existente como la carpeta de destino. El servidor de informes no crea carpetas en el sistema de archivos. La carpeta que especifique debe ser accesible a través de una conexión de red.  
  
 Compruebe que los usuarios que van a ver los informes en la carpeta compartida tengan permiso de lectura.  
  
 Cuando especifique la carpeta de destino en una suscripción, utilice el formato UNC (Convención de nomenclatura universal), que incluye el nombre de red del equipo. En la ruta de la carpeta no incluya barras diagonales inversas. El siguiente ejemplo ilustra una ruta de acceso UNC:  
  
```  
\\<servername>\reportarchive\operations\2003  
```  
  
 Cuando cree la carpeta, tenga en cuenta los límites de conexión que necesita. El servidor de informes requiere dos conexiones, pero deben incluirse las suficientes para otros usuarios que deseen abrir informes en la carpeta compartida.  
  
##  <a name="bkmk_file_formats"></a> Formatos de archivo  
 Los informes se pueden representar en diversos formatos de archivo, como HTML o Excel. Para guardar el informe en un formato de archivo específico, seleccione ese formato de representación en el momento en que cree su suscripción. Por ejemplo, si elige **Excel** , se guardará el informe como archivo de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] . Aunque puede elegir cualquier formato de representación compatible, algunos formatos funcionan mejor que otros al representar un archivo.  
  
 Para la entrega a recursos compartidos de archivos, elija un formato que entregue el informe como único archivo y que incluya todas las imágenes y el contenido relacionado en el informe. Entre los formatos adecuados se encuentran archivo web, PDF, TIFF y Excel. Evite HTML 4.0. Si su informe incluye imágenes, los formatos HTML 4.0 no las incluirán en el archivo.  
  
##  <a name="bkmk_file_options"></a> Opciones de archivo  
 Al crear una suscripción, puede elegir opciones que determinen cómo se crea el nombre del archivo y si se sustituye por versiones más recientes con el tiempo. Un nombre de archivo completo tiene tres partes: un nombre, una extensión y texto o un número que se anexa al archivo para crear un nombre de archivo exclusivo. Las opciones de sobrescritura determinan si el texto o el número se suman al nombre de archivo.  
  
 El nombre de archivo se basa en el nombre del informe, aunque es posible proporcionar un nombre personalizado en la suscripción. La extensión es opcional, pero si se especifica, el servidor de informes creará una extensión que corresponda al formato de representación.  
  
 Se pueden especificar opciones de sobrescritura a fin de volver a utilizar el mismo nombre de archivo para cada entrega de informe o para crear un archivo nuevo. Para sobrescribir el archivo, debe utilizar el mismo nombre de archivo y la misma extensión.  
  
 Un método alternativo para crear archivos exclusivos para cada entrega consiste en incluir una marca de tiempo en el nombre del archivo. Para ello, agregue el `@timestamp` variable para el nombre de archivo (por ejemplo, *CompanySales@timestamp*). De este modo, el nombre del archivo será exclusivo por definición, por lo que no se sobrescribirá nunca.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar suscripciones estándares &#40;Reporting Services en modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
