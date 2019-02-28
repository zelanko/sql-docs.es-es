---
title: Crear informes de análisis en el Asistente de experimentación de base de datos para las actualizaciones de SQL Server
description: Crear informes de análisis en el Asistente para experimentación con base de datos
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 901d410fc7aa954dcd39a852f240168f2a690e3c
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "56987691"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>Crear informes de análisis en el Asistente de experimentación de base de datos

Después de volver a reproducir el seguimiento de origen en dos de los servidores de destino, puede generar un informe de análisis en base de datos experimentación Assistant (DEA). Informes de análisis le ayudan a obtener información sobre las implicaciones de rendimiento de los cambios propuestos.

## <a name="create-an-analysis-report"></a>Crear un informe de análisis

En DEA, seleccione el icono de menú. En el menú expandido, seleccione **informes de análisis** junto al icono de la lista de comprobación.

![Menú de análisis](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

En **informes de análisis de**, seleccione **nuevo informe de análisis**.

![Nuevo menú informe de análisis](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

Escriba o seleccione la siguiente información:

- **Nombre del informe**: Escriba un nombre para el informe. Se usa el nombre del informe tanto A bases de datos de B y. Ejemplo: *A (o B)* + *nombre del informe* + *identificador único*. 
- **Nombre del servidor**: Escriba el nombre del equipo del servidor que desea incluir en A, B y las bases de datos de análisis.
- **Nombre de instancia de SQL Server**: Escriba el nombre de la instancia de SQL Server que se usará para el informe.
- **Seguimiento de servidor de origen**: Escriba el primer archivo de seguimiento (.trc) SQL Server (2008 R2).
- **Seguimiento de servidor de destino**: Especifique el destino SQL Server (2014) primer archivo .trc.

![Nueva página de informe de análisis](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>Generar un informe

Después de escribir o seleccionar la información necesaria en el **nuevo informe de análisis** página, seleccione **iniciar** para comenzar a crear el informe. Si la información que escribió es válida, se crea el informe de análisis. En caso contrario, los cuadros de texto que tienen información no válida se resaltan en rojo. Asegúrese de que escriba los valores correctos y, a continuación, seleccione **iniciar**. 

Se genera un nuevo informe de análisis. La base de datos de análisis sigue el esquema de nomenclatura análisis + *nombre del informe especificado por el usuario* + *identificador único*.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Preguntas más frecuentes acerca de los informes de análisis

### <a name="what-does-my-analysis-report-tell-me"></a>¿Qué puede revelar la mi informe de análisis?
    
DEA utiliza pruebas estadísticas para analizar la carga de trabajo y determinar cómo se ejecutó cada consulta de destino 1 a 2 de destino. Proporciona detalles de rendimiento para cada consulta. Más información sobre DEA en [comenzar](database-experimentation-assistant-get-started.md).
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>¿Puedo crear un nuevo informe de análisis mientras se está generando otro informe?
    
No.  Actualmente, solo un informe puede generarse en un momento para evitar conflictos. Sin embargo, puede ejecutar más de una captura y reproducción al mismo tiempo.

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>Actualicé DEA a la versión 2.0. ¿Puedo todavía ver y usar Mis informes antiguos?
    
Sí. Para ver los informes generados previamente, debe actualizar el esquema del informe. Para obtener más información, consulte [DEA 2.0: Actualizar el esquema de base de datos de informe de análisis de DEA](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/).
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>¿Se puede generar un informe de análisis mediante el uso de la línea de comandos?
    
Sí. Puede generar un informe de análisis en el símbolo del sistema. A continuación, puede ver el informe en la interfaz de usuario. Para obtener más información, consulte [ejecutar en el símbolo del sistema](database-experimentation-assistant-run-command-prompt.md).
    
## <a name="troubleshoot-analysis-reports"></a>Solucionar problemas de informes de análisis

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>¿Qué permisos de seguridad es necesario generar y ver un informe de análisis en mi servidor?
    
El usuario que ha iniciado sesión DEA debe tener derechos de sysadmin en el servidor de análisis. Si el usuario forma parte de un grupo, asegúrese de que el grupo tiene derechos de sysadmin.

|Posibles errores|Solución|  
|---|---|  
|No se puede conectar a la base de datos. Asegúrese de que tiene derechos de sysadmin para analizar y ver los informes.|Podría no tener derechos de acceso o el administrador del sistema en el servidor o base de datos. Confirme sus derechos de inicio de sesión y vuelva a intentarlo.|  
|No se puede generar **nombre del informe** en el servidor **nombre del servidor**. Para obtener más información, consulte el **nombre del informe** informes.|Podría no tener los derechos de administrador del sistema necesarios para generar un nuevo informe. Para ver errores detallados, seleccione el informe cerradas y compruebe los registros en % temp %\\DEA.|  
|El usuario actual no tiene los permisos necesarios para ejecutar la operación. Asegúrese de que tiene derechos de sysadmin para realizar el seguimiento y analizar los informes.|No tiene los derechos de administrador del sistema necesarios para generar un nuevo informe.|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>No puedo conectarme al equipo que ejecuta SQL Server
    
- Confirme que el nombre del equipo que ejecuta SQL Server es válido. Para confirmar, intente conectarse al servidor mediante el uso de SQL Server Management Studio (SSMS).
- Confirme que la configuración del firewall no bloquea las conexiones con el equipo que ejecuta SQL Server.
- Confirme que el usuario tiene los derechos de usuario necesarios. 

Puede ver más detalles en los registros en % temp %\\DEA. Si el problema persiste, póngase en contacto con el equipo del producto.

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>Aparece un error al generar un informe de análisis
    
Acceso a Internet es necesaria la primera vez que se genere un informe de análisis después de instalar DEA. Se requiere acceso a Internet para descargar los paquetes que son necesarios para realizar análisis estadísticos.

Si se produce un error mientras se crea el informe, la página de progreso muestra el paso específico que no se pudo generación de análisis. Puede ver más detalles en los registros en % temp %\\DEA. Compruebe que tiene una conexión válida al servidor con los derechos de usuario necesarios y, a continuación, vuelva a intentar. Si el problema persiste, póngase en contacto con el equipo del producto.

|Posibles errores|Solución|  
|---|---|  
|RInterop dio un error en Inicio. Compruebe los registros de RInterop e inténtelo de nuevo.|DEA requiere acceso a internet para descargar los paquetes de R dependientes. Compruebe los registros de RInterop en % temp %\\RInterop y DEA inicia sesión en % temp %\\DEA. Si RInterop se inicializó incorrectamente, o si inicializa sin los paquetes de R correctos, es posible que vea la excepción "No se pudo generar el nuevo informe de análisis" después del paso InitializeRInterop en los registros DEA.<br><br>Los registros de RInterop también podrían mostrar un error similar a "no hay ningún paquete jsonlite disponible." Si el equipo no tiene acceso a internet, puede descargar manualmente el paquete de R de jsonlite necesarios:<br><br><li>Vaya a % userprofile %\\DEARPackages carpeta sistema del equipo en el de archivos. Esta carpeta está formado por los paquetes que se usa R para DEA.</li><br><li>Si la carpeta jsonlite falta en la lista de los paquetes instalados, se necesita una máquina con acceso a internet para descargar la versión de lanzamiento de jsonlite\_1.4.zip desde [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html).</li><br><li>Copie el archivo .zip en la máquina donde se ejecuta DEA.  Extraiga la carpeta jsonlite y cópielo en % userprofile %\\DEARPackages. Este paso instala automáticamente el paquete jsonlite en R. La carpeta debe denominarse **jsonlite** y debe ser el contenido directamente dentro de la carpeta, no un nivel por debajo.</li><br><li>Cerrar DEA, vuelva a abrirla y análisis inténtelo de nuevo.</li><br>También puede usar el RGUI. Vaya a **paquetes** > **instalar desde el archivo zip**. Vaya al paquete que descargó anteriormente e instale.<br><br>Si RInterop se ha inicializado y configurado correctamente, debería ver "Instalar dependientes R paquete jsonlite" en los registros RInterop.|  
|No se puede conectar a la instancia de SQL Server, asegúrese de que el nombre del servidor es correcto y comprobar el acceso necesario para el usuario que ha iniciado sesión.|Podría no tener acceso o derechos de usuario para el servidor o el nombre del servidor podrían ser incorrectos.| 
|RInterop proceso agotó el tiempo de espera. Compruebe los registros DEA y RInterop, detener el proceso de RInterop en el Administrador de tareas y, a continuación, vuelva a intentarlo.<br><br>o Administrador de configuración de<br><br>RInterop está en estado de error. Detener el proceso de RInterop en el Administrador de tareas y, a continuación, vuelva a intentarlo.|Consulte los registros en % temp %\\RInterop para confirmar el error. Quitar el proceso de RInterop desde el Administrador de tareas antes de que vuelva a intentarlo. Si el problema persiste, póngase en contacto con el equipo del producto.| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>Se genera el informe, pero los datos parecen que falta
    
Compruebe la base de datos en el equipo de análisis que se está ejecutando SQL Server para confirmar la existen de datos. Compruebe que existe la base de datos de análisis y sus tablas. Por ejemplo, comprobar estas tablas: TblBatchesA, TblBatchesB y TblSummaryStats.

Si los datos no existen, es posible que los datos no ha copiado correctamente o la base de datos podría estar dañado. Si solo algunos datos no está presente, los archivos de seguimiento crean en la captura o reproducción podría no haber capturado con precisión la carga de trabajo. Si los datos están allí, compruebe los archivos de registro en % temp %\\DEA para ver si se registraron errores. A continuación, vuelva a intentar generar el informe de análisis.

¿Más preguntas o comentarios? Enviar comentarios a través de la herramienta DEA eligiendo el icono de cara sonriente en la esquina inferior izquierda.  

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo ver el informe de análisis, consulte [ver informes](database-experimentation-assistant-view-report.md).

- Para obtener una introducción minutos 19 DEA y demostración, vea el vídeo siguiente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
