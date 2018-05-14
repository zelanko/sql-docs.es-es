---
title: Tarea Limpieza de mantenimiento (Plan de mantenimiento) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.cleanup.f1
helpviewer_keywords:
- Maintenance Cleanup Task dialog box
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 689b00b0da037fd5b72d5b8785c337781cc3e0b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="maintenance-cleanup-task-maintenance-plan"></a>Tarea Limpieza de mantenimiento (Plan de mantenimiento)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice la **Tarea Limpieza de mantenimiento** para quitar archivos antiguos que estén relacionados con los planes de mantenimiento, incluidos los informes de texto creados por planes de mantenimiento y archivos de copia de seguridad de la base de datos.  
  
> [!NOTE]  
>  La tarea Limpieza de mantenimiento no elimina automáticamente archivos incluidos en las subcarpetas del directorio especificado. Esta característica reduce la posibilidad de un ataque malintencionado que utilice la tarea Limpieza de mantenimiento para eliminar archivos. Si quiere eliminar archivos en las subcarpetas de primer nivel, debe seleccionar **Incluir subcarpetas de primer nivel**.  
  
## <a name="options"></a>Opciones  
 **Conexión**  
 Muestra la conexión actual.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Archivos de copia de seguridad**  
 Elimina archivos de copia de seguridad.  
  
 **Informes de texto de plan de mantenimiento**  
 Elimina informes de texto de planes de mantenimientos ejecutados con anterioridad.  
  
 **Eliminar archivo específico**  
 Elimina el archivo específico que se indica en el cuadro **Nombre de archivo** .  
  
 **Nombre de archivo**  
 Ruta de acceso y nombre del archivo que se va a eliminar.  
  
 **Buscar en carpeta y eliminar archivos según su extensión**  
 Elimina todos los archivos con la extensión especificada de la carpeta indicada. Utilice esta opción para eliminar varios archivos a la vez, como todos los archivos de copia de seguridad con la extensión .bak, en la carpeta seleccionada.  
  
 **Carpeta**  
 Ruta de acceso y nombre de la carpeta que contiene los archivos que se van a eliminar.  
  
 **Extensión de archivo**  
 Indique la extensión de archivo de los archivos que se van a eliminar.  
  
 **Incluir subcarpetas de primer nivel**  
 Elimina archivos con la extensión especificada para **Extensión del archivo** en las subcarpetas de primer nivel, en **Carpeta**.  
  
 **Eliminar archivos en función de la antigüedad del archivo en el tiempo de ejecución de la tarea**  
 Especifique la antigüedad mínima que deben tener los archivos que quiere eliminar; para ello, especifique un número y una unidad de tiempo en el cuadro **Eliminar archivos anteriores a** .  
  
 **Eliminar archivos anteriores a**  
 Especifique la antigüedad mínima que deben tener los archivos que desea eliminar; para ello, especifique un número y una unidad de tiempo (Día, Semana, Mes o Año). Se eliminarán los archivos con una antigüedad mayor que el intervalo de tiempo especificado.  
  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  
  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **…**  
 Seleccione esta opción para ver la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Se conecta a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con la autenticación de Microsoft Windows.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Se conecta a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con la autenticación de SQL Server. Esta opción no está disponible.  
  
 **User name**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Ver también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
