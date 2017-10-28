---
title: "Configuración (migración) (DB2ToSQL) del proyecto | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7cc8dbd9eaf1f0cce54d142f775076d58528c4fc
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-db2tosql"></a>Configuración del proyecto (migración) (DB2ToSQL)
La página de migración de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA migra datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
El panel de migración está disponible tanto en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** desplegable haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **migración**.  
  
## <a name="migration-engine"></a>Motor de migración  
  
|Término|Definición|  
|--------|--------------|  
|**Motor de migración**|Especifica el motor de base de datos utilizado durante la migración de datos. Migración de datos del lado cliente se refiere al cliente SSMA recuperar los datos de origen y masiva insertar datos en SQL Server. Migración de datos del lado servidor se refiere a SSMA datos migración engine (programa de copia masiva) en el cuadro de SQL Server como un trabajo del Agente SQL recuperan datos del origen de e insertando directamente en SQL Server, lo que evita un cliente-salto adicional (un mejor rendimiento).<br /><br />**Modo predeterminado**: motor de migración de datos de lado cliente<br /><br />**Modo optimista**: motor de migración de datos de lado cliente<br /><br />**Modo completo**: motor de migración de datos de lado cliente|  
  
> [!IMPORTANT]  
> Cuando el **motor de migración de** opción está establecida en **motor de migración de datos de lado servidor**, un nuevo proyecto de opción de configuración **motor de migración de datos de lado de servidor de uso 32 bits** se muestra. Especifica si la utilidad de programa de copia masiva (BCP) de 32 bits o 64 bits se usa para migrar los datos.  
  
## <a name="miscellaneous-options"></a>Otras opciones  
  
|Término|Definición|  
|--------|--------------|  
|**Tamaño del lote**|Especifica el lote de tamaño que se usa durante la migración de datos.<br /><br />**Modo predeterminado**: 10000<br /><br />**Modo optimista**: 10000<br /><br />**Modo completo**: 10000|  
|**Restricciones CHECK**|Especifica si SSMA debe comprobar restricciones cuando inserta datos en tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Tiempo de espera de migración de datos**|Especifica el tiempo de espera que se utiliza durante la migración de datos<br /><br />**Modo predeterminado**: 15<br /><br />**Modo optimista**: 15<br /><br />**Modo completo**: 15|  
|**Opciones de migración de datos extendidos**|Muestra opciones de migración de datos adicionales para cada tabla en la pestaña de detalle independiente.<br /><br />**Modo predeterminado**: ocultar<br /><br />**Modo optimista**: ocultar<br /><br />**Modo completo**: ocultar|  
|**Activar desencadenadores**|Especifica si SSMA debe activar desencadenadores de inserción cuando agrega datos a tablas de SQL Server.<br /><br />**Modo predeterminado**: False<br /><br />**Modo optimista**: False<br /><br />**Modo completo**: False|  
|**Mantener valores de identidad**|Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a SQL Server, independientemente de los valores predeterminados que se especifican en SQL Server.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: False|  
|**Mantener valores NULL**|Especifica si SSMA conserva valores null en los datos de origen cuando agrega datos a SQL Server, independientemente de los valores predeterminados que se especifican en SQL Server.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
|**Marcar la operación de recorte de cadena con error**|Si el tamaño de la columna de destino es menor que la longitud de la cadena de origen, el valor se recorta y se marcará como error.<br /><br />**Modo predeterminado**: Sí<br /><br />**Modo optimista**: Sí<br /><br />**Modo completo**: Sí|  
|**Al producirse un error**|Detiene la migración de datos cuando se produce un error. Tiene tres opciones:<br /><br />**Detener la migración:** detiene la operación de migración de datos<br /><br />**Continúe con la siguiente tabla:** detiene la migración de datos a la tabla actual y avanza al siguiente<br /><br />**Vaya al siguiente lote:** detiene la migración de datos en el lote actual y avanza al siguiente<br /><br />**Modo predeterminado**: continuar con el siguiente lote<br /><br />**Modo optimista**: continuar con el siguiente lote<br /><br />**Modo completo**: continuar con el siguiente lote|  
|**Reemplace las fechas no compatibles**|Especifica si SSMA debe corregir las fechas anteriores a la más antigua [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** fecha (01 de enero de 1753).<br /><br />Para mantener los valores de fecha actual, seleccione **no hacen nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]no aceptará las fechas anteriores 01 de enero de 1753 en una columna de fecha y hora. Si utiliza las fechas anteriores, debe convertir los valores de fecha y hora a valores de caracteres.<br /><br />Para convertir las fechas anteriores 01 de enero de 1753 a NULL, seleccione **reemplace con NULL**.<br /><br />Para reemplazar las fechas anteriores 01 de enero de 1753 con una fecha admitida, seleccione **reemplazar con más cercano de fecha admitido**.<br /><br />**Modo predeterminado**: no hacer nada<br /><br />**Modo optimista**: no hacer nada<br /><br />**Modo completo**: reemplazar con más cercano de fecha admitido|  
|**Bloqueo de tabla**|Especifica si SSMA bloquea las tablas cuando agrega datos a tablas durante la migración de datos. Obtiene un bloqueo de actualización masiva durante la operación de copia masiva. Si el valor es False, se establece un bloqueo en el nivel de fila.<br /><br />**Modo predeterminado**: True<br /><br />**Modo optimista**: True<br /><br />**Modo completo**: True|  
  
## <a name="parallel-data-migration"></a>Migración de datos en paralelo  
  
|Término|Definición|  
|--------|--------------|  
|**Modo de migración de datos en paralelo**|Especifica el modo utilizado para los subprocesos de bifurcación para permitir la migración de datos en paralelo. En el modo Auto, SSMA elige el número de subprocesos (10 de forma predeterminada) bifurcado para migrar los datos. En el modo personalizado, el usuario puede especificar el número de subprocesos bifurcado para migrar datos (valor mínimo es 1 y el máximo es 100). Actualmente, motor de migración cliente lado datos solo admite la migración de datos en paralelo.<br /><br />**Modo predeterminado**: automático<br /><br />**Modo optimista**: automático<br /><br />**Modo completo**: automático|  
  
> [!IMPORTANT]  
> Cuando el **modo de migración de datos paralelo** opción está establecida en **personalizado**, un nuevo proyecto de opción de configuración **el número de subprocesos** se muestra. Especifica el número de subprocesos usados para la migración de datos.  
  

