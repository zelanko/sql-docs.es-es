---
title: Configuración (migración) (SybaseToSQL) del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 82f8857f-7ab1-4738-ab6e-b1e95ea94924
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ff7d8035fef2e766c598231b43f667355b088688
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394705"
---
# <a name="project-settings-migration-sybasetosql"></a>Configuración del proyecto (migración) (SybaseToSQL)
La página de migración de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA migra los datos desde Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
El panel de la migración está disponible tanto en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para los que es necesaria para ver o cambiar de configuración  **Versión de destino de migración** desplegable clic **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Migración**.  
  
## <a name="date-correction-options"></a>Opciones de corrección de fecha  
  
|Término|Definición|  
|--------|--------------|  
|**Reemplazar las fechas no compatibles**|Especifica si SSMA debería corregir las fechas anteriores a la primera [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** fecha (01 de enero de 1753).<br /><br />Para conservar los valores de fecha actual, seleccione **no hacen nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aceptará las fechas anteriores 01 de enero de 1753 en una columna de fecha y hora. Si usa las fechas anteriores, debe convertir los valores de fecha y hora para los valores de caracteres.<br /><br />Para convertir las fechas anteriores 01 de enero de 1753 a NULL, seleccione **reemplace con NULL**.<br /><br />Para reemplazar las fechas anteriores 01 de enero de 1753 con una fecha admitida, seleccione **reemplazar con más cercano de fecha admitido**.<br /><br />**Modo predeterminado**: no hacer nada<br /><br />**Modo optimista**: no hacer nada<br /><br />**Modo completo**: reemplazar con más cercano de fecha admitido|  
  
## <a name="migration-engine"></a>Motor de migración  
  
|Término|Definición|  
|--------|--------------|  
|**Motor de migración**|Especifica utilizada durante la migración de datos de motor de base de datos. Migración de datos del lado cliente se refiere al cliente SSMA recuperar los datos de origen y de insertar datos en SQL Server de forma masiva. Migración de datos del lado servidor se refiere a SSMA datos motor de migración (programa de copia masiva) que se ejecutan en el cuadro de SQL Server como un trabajo del Agente SQL al recuperar datos desde el origen e insertar directamente en SQL Server, lo que evita un cliente de-salto adicional (un mejor rendimiento).<br /><br />**Modo predeterminado**: motor de migración de datos de lado cliente<br /><br />**Modo optimista**: motor de migración de datos de lado cliente<br /><br />**Modo completo**: motor de migración de datos de lado cliente|  
  
> [!IMPORTANT]  
> Cuando el **migración motor** opción está establecida en **motor de migración de datos de lado servidor**, un nuevo proyecto, establecer la opción **motor de migración de datos de uso 32 bits Server lado** se muestra . Especifica si se usa la utilidad de programa de copia masiva (BCP) de 32 bits o 64 bits para migrar los datos.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
  
|Término|Definición|  
|--------|--------------|  
|**Tamaño de lote**|Especifica el lote de tamaño que se usa durante la migración de datos.<br /><br />**Modo predeterminado**: 10000<br /><br />**Modo optimista**: 10000<br /><br />**Modo completo**: 10000|  
|**Restricciones CHECK**|Especifica si SSMA debe comprobar restricciones cuando inserta datos en tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Tiempo de espera de migración de datos**|Especifica el tiempo de espera utilizado durante la migración de datos<br /><br />**Modo predeterminado**: 15<br /><br />**Modo optimista**: 15<br /><br />**Modo completo**: 15|  
|**Opciones de migración de datos extendidos**|Muestra las opciones de migración de datos adicionales para cada tabla en la pestaña Detalles independientes.<br /><br />**Modo predeterminado**: ocultar<br /><br />**Modo optimista**: ocultar<br /><br />**Modo completo**: ocultar|  
|**Activar desencadenadores**|Especifica si SSMA debe activar desencadenadores de inserción cuando agrega datos a tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Mantener valores de identidad**|Especifica si SSMA conserva los valores de identidad de Sybase cuando agrega datos a SQL Server. Un valor False hace que los valores de identidad que se asignará el destino.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Mantener valores NULL**|Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a SQL Server, independientemente de los valores predeterminados que se especifican en SQL Server.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Al producirse un error**|Detiene la migración de datos cuando se produce un error. Tiene tres opciones:<br /><br />**Detener la migración:** detiene la operación de migración de datos<br /><br />**Continúe con la siguiente tabla:** deja de migración de datos a la tabla actual y avanza a la siguiente<br /><br />**Vaya al siguiente lote:** deja de migración de datos para el lote actual y avanza a la siguiente<br /><br />**Modo predeterminado**: continúe con el siguiente lote<br /><br />**Modo optimista**: continúe con el siguiente lote<br /><br />**Modo completo**: continúe con el siguiente lote|  
|**Redondear parte fraccionaria de números**|Especifica si se debe recortar las fracciones de datos decimal y numeric durante la migración a tipos enteros o mostrar el mensaje de error si la parte fraccionaria es no trivial<br /><br />**Modo predeterminado**: N<br /><br />**Modo optimista**: N<br /><br />**Modo completo**: N|  
|**Sybase Unicode Endian**|Especifica el tipo de endian para las cadenas Sybase Unicode. Para esta configuración concreta, se pueden establecer las siguientes opciones:<br /><br />Little-endian<br /><br />Big-endian<br /><br />**Modo predeterminado**: Little-endian<br /><br />**Modo optimista**: Little-endian<br /><br />**Modo completo**: Little-endian|  
|**Bloqueo de tabla**|Especifica si SSMA bloquea las tablas cuando agrega datos a las tablas durante la migración de datos. Obtiene un bloqueo de actualización masiva para la duración de la operación de copia masiva. Si el valor es False, se establece un bloqueo en el nivel de fila.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Usar cursores**|Se recuperan los datos de uso de cursores si establece esta opción de base de datos de origen.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
  
## <a name="parallel-data-migration"></a>Migración de datos paralelos  
  
|Término|Definición|  
|--------|--------------|  
|**Modo de migración de datos paralelos**|Especifica el modo utilizado para los subprocesos de bifurcación para habilitar la migración de datos en paralelo. En el modo Auto, SSMA elige el número de subprocesos (10 de forma predeterminada) bifurcado para migrar los datos. En el modo personalizado, el usuario puede especificar el número de subprocesos bifurcado para migrar datos (valor mínimo es 1 y el máximo es 100). Actualmente, motor de migración cliente lado datos solo admite la migración de datos en paralelo.<br /><br />**Modo predeterminado**: automática<br /><br />**Modo optimista**: automática<br /><br />**Modo completo**: automática|  
  
> [!IMPORTANT]  
> Cuando el **modo de migración de datos paralelo** opción está establecida en **personalizado**, un nuevo proyecto, establecer la opción **el número de subprocesos** se muestra. Especifica el número de subprocesos usados para la migración de datos.  
  
