---
title: Página Cargar archivo (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bb3166f-9374-4449-b66a-ffb77298507d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1100baa3cd72a04d208b2076d91ca4efed7d38e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098867"
---
# <a name="upload-file-page-report-manager"></a>Cargar archivo (página del Administrador de informes)
  Use la página Cargar archivo para publicar un archivo del sistema de archivos en la base de datos del servidor de informes. Los archivos cargados se representan como elementos en la jerarquía de carpetas del servidor de informes.  
  
-   Los archivos .rdl cargados se publican como informes en el servidor de informes.  
  
-   Los archivos .smdl cargados se publican como modelos de informe si contienen información de la vista del origen de datos. Si les falta una referencia de vista del origen de datos, se produce un error durante la carga. Es posible que falte información de la vista del origen de datos si se carga un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] archivo. SMDL desde un proyecto de modelos de informe. En los proyectos de modelo de informe, la información de la vista del origen de datos se almacena en un archivo independiente en lugar de hacerlo en el mismo archivo .smdl.  
  
     Los archivos de modelo que no contienen información de vista del origen de datos (y que por tanto se cargan correctamente) son aquellos que se han publicado previamente en un servidor de informes y se han guardado posteriormente del servidor a un archivo del sistema de archivos. Si abre la página Propiedades generales de un modelo y hace clic en **Editar** para abrirlo, puede guardarlo en un archivo y, a continuación, cargarlo como un nuevo modelo en el servidor de informes. El archivo .SMDL que cargue posteriormente dispondrá de toda la información necesaria para la publicación de modelos.  
  
-   Todos los demás tipos de archivo que se cargan se almacenan como recursos. Esto incluye archivos .rds que contienen información de conexión del origen de datos de informe. Al cargar un archivo .rds no se genera un elemento de origen de datos compartidos en el servidor de informes.  
  
 Al cargar un elemento, se coloca en la carpeta actual. Una vez finalizada la carga, el elemento se puede mover a una ubicación diferente.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-upload-file-page"></a>Para abrir la página Cargar archivo  
  
1.  Abra el Administrador de informes y desplácese hasta la carpeta en la que desea cargar un archivo.  
  
2.  En la barra de herramientas, haga clic en **Cargar archivo**.  
  
## <a name="options"></a>Opciones  
 **Archivo para cargar**  
 Muestra la ruta de acceso completa del archivo que se va a copiar desde el sistema de archivos.  
  
 **Browse**  
 Haga clic para elegir un archivo del sistema de archivos.  
  
 **Nombre**  
 Escriba el nombre del archivo tal como desea que aparezca en el espacio de nombres del servidor de informes. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios en blanco y algunos símbolos. No use los caracteres ; ? : \@ & = +, $ * \< > | "o/al especificar un nombre de elemento.  
  
 **Sobrescribir elemento si existe**  
 Active esta casilla si desea reemplazar un elemento por una versión más reciente. Para que se sobrescriba una versión existente, deben coincidir exactamente el nombre del elemento nuevo y el nombre del elemento existente.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes de &#40;de página de contenido&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Administrador de informes la ayuda F1](../../2014/reporting-services/report-manager-f1-help.md)   
 [Cargar archivos a una carpeta](report-server/upload-files-to-a-folder.md)  
  
  
