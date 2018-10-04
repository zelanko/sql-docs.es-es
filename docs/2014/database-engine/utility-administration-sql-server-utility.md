---
title: Administración de la utilidad (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6da38b25ca23302c8b683a5c9b54ed2b6f88f6b2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128845"
---
# <a name="utility-administration-sql-server-utility"></a>Administración de la utilidad (utilidad de SQL Server)
  Utilice las pestañas Administración de la utilidad para administrar la configuración de directivas, la seguridad y el almacenamiento de datos de una utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obtener más información sobre conceptos de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Pestaña Directiva: utilice la pestaña de directivas para ver o especificar las directivas globales de supervisión.  
  
 Establezca directivas globales de supervisión de aplicaciones de capas de datos. Para expandir la lista de valores correspondiente a esta opción, haga clic en la flecha junto al nombre de la directiva o haga clic en el título de la directiva.  
 ¿Cuándo se queda una aplicación sin capacidad de procesamiento? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador es 0%.  
  
 ¿Cuándo se queda una aplicación sin espacio para archivos? Para cambiar la directiva correspondiente a la utilización del espacio de un archivo de datos o un archivo de registro, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de archivos es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de archivos es 0%.  
  
 Establezca las directivas globales de supervisión de aplicaciones de instancias administradas de SQL Server. Para expandir la lista de valores correspondiente a esta opción, haga clic en la flecha junto al nombre de la directiva o haga clic en el título de la directiva.  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin capacidad de procesamiento? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador de instancias es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador de instancias es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin capacidad de procesamiento en el sistema informático? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador del sistema informático es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador del sistema informático es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin espacio para archivos? Para cambiar la directiva correspondiente a la utilización del espacio de un archivo de datos o un archivo de registro, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de archivos es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de archivos es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sin espacio de volumen de almacenamiento en el equipo? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de volumen en el sistema informático es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de volumen en el sistema informático es 0%.  
  
 Reducción del ruido que provoca la infracción de directivas en recursos muy volátiles. Para expandir los controles correspondientes a esta característica, haga clic en la flecha hacia abajo a la derecha de la pantalla.  
 Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;utilidad de SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Pestaña Seguridad: muestra los nombres de inicio de sesión con permisos para administrar el UCP o poder leer desde él.  
  
 Seleccione los inicios de sesión del UCP que se agregarán al rol Lector de utilidad.  
 Los privilegios del rol Lector de utilidad hacen posible que la cuenta de usuario:  
  
-   Se conecte a la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Vea todos los puntos de vista en el explorador de la utilidad en SSMS.  
  
-   Vea los valores de configuración en el nodo Administración de la utilidad en el explorador de la utilidad en SSMS.  
  
 Los administradores de la utilidad pueden inscribir instancias de SQL Server y quitar instancias de SQL Server de una Utilidad de SQL Server, así como modificar directivas en instancias administradas y valores de administración en el UCP.  
  
 Para ser administrador de la utilidad, debe disponer de privilegios sysadmin en la instancia de SQL Server. Para agregar o cambiar las cuentas de usuario para el UCP de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], utilice Explorador de objetos en SSMS con el fin de agregar al usuario a los inicios de sesión del servidor de la instancia de UCP de SQL Server. Para obtener más información, vea [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql).  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Pestaña Almacenamiento de datos: muestra los detalles de configuración para el almacén de administración de datos de la utilidad.  
  
 Retención de datos  
 Especifique el período de retención de datos para obtener la información de utilización que se haya recopilado para las instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. El período predeterminado es 1 año. El valor mínimo es de 1 mes. El valor máximo admitido es 2 años.  
  
 Información de configuración de almacenamiento de datos de utilidad  
 Los siguientes valores de configuración no se pueden establecer en esta versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Nombre de UMDW: Sysutility_mdw_\<GUID>_DATA.  
  
-   Frecuencia de la carga del conjunto de recopilación: cada 15 minutos.  
  
 El directorio de UMDW se puede configurar: \<Unidad del sistema:>:Archivos de programa\Microsoft SQL Server\MSSQL10_50.<Nombre_UCP\MSSQL\Data\\,donde \<Unidad del sistema> normalmente es la unidad C:\. El archivo de registro, UMDW_\<GUID>_LOG, se encuentra en el mismo directorio.  
  
> [!NOTE]  
>  La ubicación del archivo del almacén de administración de datos de utilidad se puede cambiar mediante detach/attach o ALTER DATABASE. Recomendamos el uso de ALTER DATABASE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Restablecer los valores originales  
 Para restablecer los valores de esta pestaña a los valores predeterminados, haga clic en el botón **Restaurar valores predeterminados** y, luego, en **Aplicar**.  
  
## <a name="see-also"></a>Vea también  
 [Panel de la utilidad &#40;utilidad de SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
