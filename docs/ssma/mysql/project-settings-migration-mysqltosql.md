---
title: Configuración (migración) (MySQLToSQL) del proyecto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4a423404a8f5db4e20331c3b187365a889bea48a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261819"
---
# <a name="project-settings-migration-mysqltosql"></a>Configuración del proyecto (migración) (MySQLToSQL)
La página de migración de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA migra los datos desde MySQL a SQL Server.  
  
El panel de la migración está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto en **versión de destino de migración** lista desplegable de que desea tener acceso a la configuración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Migración**.  
  
## <a name="options"></a>Opciones  
  
### <a name="bulk-copy"></a>Copia masiva  
  
|Término|Definición|  
|--------|--------------|  
|**Tamaño de lote**|Especifica el lote de tamaño que se usa durante la migración de datos.<br /><br />**Modo predeterminado**:  1000<br /><br />**Modo optimista**:  1000<br /><br />**Modo completo**:  1000|  
|**Restricciones CHECK**|Especifica si SSMA debe comprobar restricciones cuando inserta datos en tablas de SQL Server.<br /><br />**Modo predeterminado**:  False<br /><br />**Modo optimista**:  False<br /><br />**Modo completo**:  False|  
|**Activar desencadenadores**|Especifica si SSMA debe activar desencadenadores de inserción cuando agrega datos a tablas de SQL Server.<br /><br />**Modo predeterminado**:  False<br /><br />**Modo optimista**:  False<br /><br />**Modo completo**:  False|  
|**Mantener valores de identidad**|Especifica si SSMA conserva los valores de identidad de MySQL cuando agrega datos a SQL Server. Un valor False hace que los valores de identidad que se asignará el destino.<br /><br />**Modo predeterminado**:  True<br /><br />**Modo optimista**:  True<br /><br />**Modo completo**:  True|  
|**Mantener valores NULL**|Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a SQL Server, independientemente de los valores predeterminados que se especifican en SQL Server.<br /><br />**Modo predeterminado**:  True<br /><br />**Modo optimista**:  True<br /><br />**Modo completo**:  True|  
|**Bloqueo de tabla**|Especifica si SSMA bloquea las tablas cuando agrega datos a las tablas durante la migración de datos. Obtiene un bloqueo de actualización masiva para la duración de la operación de copia masiva. Si el valor es False, se establece un bloqueo en el nivel de fila.<br /><br />**Modo predeterminado**:  False<br /><br />**Modo optimista**:  False<br /><br />**Modo completo**:  False|  
  
### <a name="data-modification"></a>Modificación de datos  
  
|Término|Definición|  
|--------|--------------|  
|**Migración de fechas no válidas**|Especifica cómo se migran las fechas no válidas con como ' 2007-04-23' o ' 2000-06-31 10:00:00 ' en formatos de fecha y la fecha y hora.<br /><br />**Modo predeterminado**:  Establecer en NULL<br /><br />**Modo optimista**:  Establecer en NULL<br /><br />**Modo completo**:  Establecer en NULL|  
|**Valores de tiempo negativos migración**|Especifica cómo migrar los valores negativos como '-30:11:00' en las columnas de tiempo.<br /><br />**Modo predeterminado**:  Establecer en NULL<br /><br />**Modo optimista**:  Establecer en NULL<br /><br />**Modo completo**:  Establecer en NULL|  
|**Valores de tiempo en 24 horas de migración**|Especifica cómo migrar los valores de tiempo de más de ' 23:59:59 ' en las columnas de tiempo.<br /><br />**Modo predeterminado**:  Establecer en NULL<br /><br />**Modo optimista**:  Establecer en NULL<br /><br />**Modo completo**:  Establecer en NULL|  
|**Truncar los valores binarios para caber en la columna**|En caso afirmativo, SSMA trunca los valores binarios de MySQL que no caben en columnas de tablas SQL y genera el mensaje de error adecuado. Si No, produce un error en la fila<br /><br />**Modo predeterminado**:  No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:  No|  
|**Truncar los valores de caracteres para caber en la columna**|SSMA trunca los valores de caracteres de MySQL que no caben en columnas de tablas SQL y genera el mensaje de error adecuado.<br /><br />**Modo predeterminado**:  No<br /><br />**Modo optimista**:  No<br /><br />**Modo completo**:  No|  
|**Migración de cero fechas**|Especifica cómo se migran las fechas de cero, como ' 0000-00-00' o ' 0000-00-00 00:00:00 ' en las columnas DATE y DATETIME.<br /><br />**Modo predeterminado**:  Establecer en NULL<br /><br />**Modo optimista**:  Establecer en NULL<br /><br />**Modo completo**:  Establecer en NULL|  
|**Cero en la migración de fechas**|Especifica cómo se migran las fechas con cero elementos, como ' 2009-01: 00' o ' 2000-00-00-11:00:00 ' en las columnas DATE y DATETIME.<br /><br />**Modo predeterminado**:  Establecer en NULL<br /><br />**Modo optimista**:  Establecer en NULL<br /><br />**Modo completo**:  Establecer en NULL|  
  
### <a name="migration-engine"></a>Motor de migración  
  
|Término|Definición|  
|--------|--------------|  
|**Motor de migración**|Especifica utilizada durante la migración de datos de motor de base de datos. Migración de datos del lado cliente se refiere al cliente SSMA recuperar los datos de origen y de insertar datos en SQL Server de forma masiva. Migración de datos del lado servidor se refiere a SSMA datos motor de migración (programa de copia masiva) que se ejecutan en el cuadro de SQL Server como un trabajo del Agente SQL al recuperar datos desde el origen e insertar directamente en SQL Server, lo que evita un cliente de-salto adicional (un mejor rendimiento).<br /><br />**Modo predeterminado**:  Motor de migración de datos de lado cliente<br /><br />**Modo optimista**:  Motor de migración de datos de lado cliente<br /><br />**Modo completo**:  Motor de migración de datos de lado cliente|  
  
> [!IMPORTANT]  
> Cuando el **migración motor** opción está establecida en **motor de migración de datos de lado servidor**, un nuevo proyecto, establecer la opción **motor de migración de datos de uso 32 bits Server lado** se muestra . Especifica si se usa la utilidad de programa de copia masiva (BCP) de 32 bits o 64 bits para migrar los datos.  
  
### <a name="misc"></a>Varios  
  
|Término|Definición|  
|--------|--------------|  
|**Opciones de migración de datos extendidos**|Muestra las opciones de migración de datos adicionales para cada tabla en la pestaña Detalles independientes.<br /><br />**Modo predeterminado**:  Ocultar<br /><br />**Modo optimista**:  Ocultar<br /><br />**Modo completo**:  Ocultar|  
|**Al producirse un error**|Detiene la migración de datos cuando se produce un error. Tiene tres opciones:<br /><br />**Detener la migración:** Operación de migración de datos se detiene<br /><br />**Continúe con la tabla siguiente:** Detiene la migración de datos a la tabla actual y avanza a la siguiente<br /><br />**Continúe con el siguiente lote:** Detiene la migración de datos para el lote actual y avanza a la siguiente<br /><br />**Modo predeterminado**: Continúe con el siguiente lote<br /><br />**Modo optimista**: Continúe con el siguiente lote<br /><br />**Modo completo**: Continúe con el siguiente lote|  
  
### <a name="parallel-data-migration"></a>Migración de datos paralelos  
  
|Término|Definición|  
|--------|--------------|  
|**Modo de migración de datos paralelos**|Especifica el modo utilizado para los subprocesos de bifurcación para habilitar la migración de datos en paralelo. En el modo Auto, SSMA elige el número de subprocesos (10 de forma predeterminada) bifurcado para migrar los datos. En el modo personalizado, el usuario puede especificar el número de subprocesos bifurcado para migrar datos (valor mínimo es 1 y el máximo es 100). Actualmente, motor de migración cliente lado datos solo admite la migración de datos en paralelo.<br /><br />**Modo predeterminado**:  Auto<br /><br />**Modo optimista**:  Auto<br /><br />**Modo completo**:  Auto|  
  
> [!IMPORTANT]  
> Cuando el **modo de migración de datos paralelo** opción está establecida en **personalizado**, un nuevo proyecto, establecer la opción **el número de subprocesos** se muestra. Especifica el número de subprocesos usados para la migración de datos.  
  
### <a name="spatial-data"></a>Datos espaciales  
  
|Término|Definición|  
|--------|--------------|  
|**Control de errores**|Especifica cómo controlar los errores de migración de los valores de tipos de datos espaciales. Si se especifica 'Reemplace con NULL', todos los valores espaciales, lo que produce errores se reemplazará con el valor NULL. Ningún reemplazo se realiza en caso contrario.<br /><br />**Modo predeterminado**:  Generar un Error<br /><br />**Modo optimista**:  Generar un Error<br /><br />**Modo completo**:  Generar un Error|  
|**Validación de valor**|Especifica cómo controlar valores espaciales no válidos. Si se especifica 'Intente realizar válido', que se va a se realiza un intento para modificar los valores no válidos para que sean válidos.<br /><br />**Modo predeterminado**: Convertir válida<br /><br />**Modo optimista**: No cambie<br /><br />**Modo completo**: Convertir válida|  
  
