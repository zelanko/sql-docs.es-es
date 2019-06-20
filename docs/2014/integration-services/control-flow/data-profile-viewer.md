---
title: Visor de perfil de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], output viewer
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0f6bcad3636178fb4aebbcdbeee29ba2542f092e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832420"
---
# <a name="data-profile-viewer"></a>Visor de perfil de datos
  El paso siguiente del proceso de generación de perfiles de datos consiste en ver y analizar los perfiles de datos. Estos perfiles pueden verse después de ejecutar la tarea de generación de perfiles de datos dentro de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y de calcular los perfiles de datos. Para más información sobre cómo configurar y ejecutar las tareas de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](data-profiling-task.md).  
  
> [!IMPORTANT]  
>  El archivo de salida podría contener datos confidenciales acerca de la base de datos y de los datos que contiene. Para conocer sugerencias sobre cómo mejorar la seguridad del archivo, vea [Acceso a los archivos usados por los paquetes](../access-to-files-used-by-packages.md).  
  
## <a name="data-profiles"></a>Perfiles de datos  
 Para ver los perfiles de datos, se configura la tarea de generación de perfiles de datos de modo que envíe su salida a un archivo y, a continuación, se utiliza el Visor de perfil de datos independiente. Para abrir el Visor de perfil de datos, realice una de las acciones siguientes.  
  
-   Haga clic con el botón derecho en la tarea **Generación de perfiles de datos** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] y, después, haga clic en **Editar**. Haga clic en **Abrir el visor de perfil** en la página **General** del **Editor de tareas de generación de perfiles de datos**.  
  
-   En la carpeta *\<unidad>*:\Archivos de programa (x86) | Archivos de programa\Microsoft SQL Server\110\DTS\Binn, ejecute DataProfileViewer.exe.  
  
 El visor utiliza varios paneles para mostrar los perfiles solicitados y los resultados calculados, y también permite la obtención de detalles:  
  
 Panel**Perfiles**   
 En el panel **Perfiles** se muestran los perfiles que se han pedido en la tarea de generación de perfiles de datos. Para ver los resultados calculados para el perfil, selecciónelo en el panel **Perfiles** y los resultados aparecerán en los otros paneles del visor.  
  
 Panel**Resultados**   
 El panel **Resultados** usa una única fila para resumir los resultados calculados del perfil. Por ejemplo, si se solicita un **Perfil de distribución de longitud de columnas**, esta fila incluye la longitud mínima, la máxima y el recuento de filas. Para la mayoría de los perfiles, es posible seleccionar esta fila en el panel **Resultados** con objeto de ver los detalles adicionales en el panel **Detalles** opcional.  
  
 Panel**Detalles**   
 Para la mayoría de los tipos de perfiles, en el panel **Detalles** se muestra información adicional sobre los resultados del perfil seleccionados en el panel **Resultados** . Por ejemplo, si solicita un **Perfil de distribución de longitud de columnas**, el panel **Detalles** muestra cada una de las longitudes de columna que se han hallado. El panel también muestra el número y el porcentaje de filas cuyo valor de columna tiene esa longitud de columna.  
  
 Para los tres tipos de perfil que se calculan sobre varias columnas (Clave candidata, Dependencia funcional e Inclusión de valores), en el panel **Detalles** se muestran las infracciones de la relación esperada. Por ejemplo, si se solicita un Perfil de claves candidatas, el panel Detalles muestra los valores duplicados que infringen la unicidad de la clave candidata.  
  
 Si el origen de datos que se usa para calcular el perfil está disponible, puede hacer doble clic en una fila en el panel **Detalles** para ver las filas de datos coincidentes en el panel **Obtención de detalles** .  
  
 Panel**Obtención de detalles**   
 Puede hacer doble clic en una fila del panel **Detalles** para ver las filas coincidentes de datos en el panel **Obtención de detalles** cuando se cumplen las condiciones siguientes:  
  
-   El origen de datos que se utiliza para calcular el perfil está disponible.  
  
-   Tiene permiso para ver los datos.  
  
 Para conectarse a la base de datos de origen y realizar una solicitud de obtención de detalles, el Visor de perfil de datos usa la autenticación de Windows y las credenciales del usuario actual. El Visor de perfil de datos no utiliza la información de conexión que está almacenada en el paquete que ejecutó la tarea de generación de perfiles de datos.  
  
> [!IMPORTANT]  
>  La capacidad de detalle, que está disponible en el Visor de perfil de datos, envía las consultas actuales al origen de datos original. Estas consultas pueden tener un efecto desfavorable en el rendimiento del servidor.  
>   
>  Si obtiene los detalles de un archivo de salida que no se ha creado recientemente, las consultas de detalle podrían devolver un conjunto diferente de filas al que se usó para calcular la salida original.  
  
 Para obtener más información sobre la interfaz de usuario del Visor de perfil de datos, vea [Data Profile Viewer F1 Help](../data-profile-viewer-f1-help.md).  
  
  
