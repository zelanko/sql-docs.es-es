---
title: "Configuración (migración) (MySQLToSQL) del proyecto | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 97ea6eb0162b544f3c0666042b0ae70a5783fe43
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-migration-mysqltosql"></a>Configuración del proyecto (migración) (MySQLToSQL)
La página de migración de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA migra datos de MySQL a SQL Server.  
  
El panel de migración está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto en **versión de destino de migración** de lista desplegable del que desea obtener acceso a la configuración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
## <a name="options"></a>.  
  
### <a name="bulk-copy"></a>Copia masiva  
  
|Término|Definición|  
|--------|--------------|  
|**Tamaño del lote**|Especifica el lote de tamaño que se usa durante la migración de datos.<br /><br />**Modo predeterminado**: 1000<br /><br />**Modo optimista**: 1000<br /><br />**Modo completo**: 1000|  
|**Restricciones CHECK**|Especifica si SSMA debe comprobar restricciones cuando inserta datos en tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Activar desencadenadores**|Especifica si SSMA debe activar desencadenadores de inserción cuando agrega datos a tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Mantener valores de identidad**|Especifica si SSMA conserva los valores de identidad de MySQL cuando agrega datos a SQL Server. Un valor de False hace que los valores de identidad que se asignará el destino.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Mantener valores NULL**|Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a SQL Server, independientemente de los valores predeterminados que se especifican en SQL Server.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Bloqueo de tabla**|Especifica si SSMA bloquea las tablas cuando agrega datos a tablas durante la migración de datos. Obtiene un bloqueo de actualización masiva durante la operación de copia masiva. Si el valor es False, se establece un bloqueo en el nivel de fila.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
  
### <a name="data-modification"></a>Modificación de datos  
  
|Término|Definición|  
|--------|--------------|  
|**Migración de fechas no válidas**|Especifica cómo se migran las fechas no válidas con como ' 2007-04-23' o ' 2000-06-31 10:00:00 ' en formatos de fecha y la fecha y hora.<br /><br />**Modo predeterminado**: establecer como NULL<br /><br />**Modo optimista**: establecer como NULL<br /><br />**Modo completo**: establecer como NULL|  
|**Valores de tiempo negativos migración**|Especifica cómo se migran los valores negativos como '-30:11:00' en las columnas de tiempo.<br /><br />**Modo predeterminado**: establecer como NULL<br /><br />**Modo optimista**: establecer como NULL<br /><br />**Modo completo**: establecer como NULL|  
|**Valores de hora en 24 horas de migración**|Especifica cómo migrar los valores de tiempo de más de ' 23: 59:59' en las columnas de tiempo.<br /><br />**Modo predeterminado**: establecer como NULL<br /><br />**Modo optimista**: establecer como NULL<br /><br />**Modo completo**: establecer como NULL|  
|**Valores binarios truncados para caber en la columna**|En caso afirmativo, SSMA trunca los valores binarios de MySQL que no caben en columnas de la tabla SQL y genera el mensaje de error adecuado. En caso negativo, produce un error en la fila<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: No|  
|**Truncar los valores de caracteres para caber en la columna**|SSMA trunca los valores de carácter de MySQL que no caben en columnas de la tabla SQL y genera el mensaje de error adecuado.<br /><br />**Modo predeterminado**: No<br /><br />**Modo optimista**: No<br /><br />**Modo completo**: No|  
|**Cero migración de fechas**|Especifica cómo se migran cero fechas como ' 0000: 00: 00' o ' 0000: 00-00 00:00:00 ' en las columnas de fecha y la fecha y hora.<br /><br />**Modo predeterminado**: establecer como NULL<br /><br />**Modo optimista**: establecer como NULL<br /><br />**Modo completo**: establecer como NULL|  
|**Cero en la migración de fechas**|Especifica cómo se migran las fechas con cero elementos como ' 2009-01-00' o ' 2000-00-00 11:00:00 ' en las columnas de fecha y la fecha y hora.<br /><br />**Modo predeterminado**: establecer como NULL<br /><br />**Modo optimista**: establecer como NULL<br /><br />**Modo completo**: establecer como NULL|  
  
### <a name="migration-engine"></a>Motor de migración  
  
|Término|Definición|  
|--------|--------------|  
|**Motor de migración**|Especifica el motor de base de datos utilizado durante la migración de datos. Migración de datos del lado cliente se refiere al cliente SSMA recuperar los datos de origen y masiva insertar datos en SQL Server. Migración de datos del lado servidor se refiere a SSMA datos migración engine (programa de copia masiva) en el cuadro de SQL Server como un trabajo del Agente SQL recuperan datos del origen de e insertando directamente en SQL Server, lo que evita un cliente-salto adicional (un mejor rendimiento).<br /><br />**Modo predeterminado**: motor de migración de datos de lado cliente<br /><br />**Modo optimista**: motor de migración de datos de lado cliente<br /><br />**Modo completo**: motor de migración de datos de lado cliente|  
  
> [!IMPORTANT]  
> Cuando el **motor de migración de** opción está establecida en **motor de migración de datos de lado servidor**, un nuevo proyecto de opción de configuración **motor de migración de datos de lado de servidor de uso 32 bits** se muestra. Especifica si la utilidad de programa de copia masiva (BCP) de 32 bits o 64 bits se usa para migrar los datos.  
  
### <a name="misc"></a>Varios  
  
|Término|Definición|  
|--------|--------------|  
|**Opciones de migración de datos extendidos**|Muestra opciones de migración de datos adicionales para cada tabla en la pestaña de detalle independiente.<br /><br />**Modo predeterminado**: ocultar<br /><br />**Modo optimista**: ocultar<br /><br />**Modo completo**: ocultar|  
|**Al producirse un error**|Detiene la migración de datos cuando se produce un error. Tiene tres opciones:<br /><br />**Detener la migración:** detiene la operación de migración de datos<br /><br />**Continúe con la siguiente tabla:** detiene la migración de datos a la tabla actual y avanza al siguiente<br /><br />**Vaya al siguiente lote:** detiene la migración de datos en el lote actual y avanza al siguiente<br /><br />**Modo predeterminado**: continuar con el siguiente lote<br /><br />**Modo optimista**: continuar con el siguiente lote<br /><br />**Modo completo**: continuar con el siguiente lote|  
  
### <a name="parallel-data-migration"></a>Migración de datos en paralelo  
  
|Término|Definición|  
|--------|--------------|  
|**Modo de migración de datos en paralelo**|Especifica el modo utilizado para los subprocesos de bifurcación para permitir la migración de datos en paralelo. En el modo Auto, SSMA elige el número de subprocesos (10 de forma predeterminada) bifurcado para migrar los datos. En el modo personalizado, el usuario puede especificar el número de subprocesos bifurcado para migrar datos (valor mínimo es 1 y el máximo es 100). Actualmente, motor de migración cliente lado datos solo admite la migración de datos en paralelo.<br /><br />**Modo predeterminado**: automático<br /><br />**Modo optimista**: automático<br /><br />**Modo completo**: automático|  
  
> [!IMPORTANT]  
> Cuando el **modo de migración de datos paralelo** opción está establecida en **personalizado**, un nuevo proyecto de opción de configuración **el número de subprocesos** se muestra. Especifica el número de subprocesos usados para la migración de datos.  
  
### <a name="spatial-data"></a>Datos espaciales  
  
|Término|Definición|  
|--------|--------------|  
|**Control de errores**|Especifica cómo controlar los errores de migración de valores de tipos de datos espaciales. Si se especifica 'Replace con NULL', todos los valores espaciales, lo que produce errores se reemplazará por un valor nulo. Ningún reemplazo se realiza en caso contrario.<br /><br />**Modo predeterminado**: generar un Error<br /><br />**Modo optimista**: generar un Error<br /><br />**Modo completo**: generar un Error|  
|**Validación del valor**|Especifica cómo controlar valores espaciales no válidos. Si se especifica 'Intente realizar válido', que se va a se realiza un intento para modificar los valores no válidos para que sean válidos.<br /><br />**Modo predeterminado**: convertir válida<br /><br />**Modo optimista**: no cambie<br /><br />**Modo completo**: convertir válida|  
  
