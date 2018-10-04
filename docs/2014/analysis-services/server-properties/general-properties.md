---
title: Propiedades generales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dab367196f1d4d80f965a2ff400fd6193b6e3508
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171185"
---
# <a name="general-properties"></a>Propiedades generales
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor descritas en las siguientes tablas. En este tema se documentan las propiedades de servidor en el archivo msmdsrv.ini que no se incluyen de otro modo en una sección concreta, como Seguridad, Red o ThreadPool. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional y tabular, a menos que se especifique lo contrario  
  
## <a name="non-specific-category"></a>Categoría no específica  
 `AdminTimeout`  
 Propiedad de entero de 32 bits con signo que define el tiempo de espera del administrador, en segundos. Se trata de una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 El valor predeterminado de esta propiedad es cero (0), que indica que no hay tiempo de espera.  
  
 `AllowedBrowsingFolders`  
 Propiedad de cadena que especifica en una lista delimitada las carpetas que se pueden examinar al guardar, abrir y buscar archivos en los cuadros de diálogo de Analysis Services. La cuenta de servicio de Analysis Services debe tener permisos de lectura y escritura en cualquiera de las carpetas que agregue a la lista.  
  
 `BackupDir`  
 Propiedad de cadena que identifica el nombre del directorio en el que se almacenan de manera predeterminada los archivos de copia de seguridad, en caso de que no se especifique ninguna ruta de acceso como parte del comando Backup.  
  
 `CollationName`  
 Propiedad de cadena que identifica la intercalación del servidor. Para más información, vea [Idiomas e intercalaciones &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md).  
  
 `CommitTimeout`  
 Propiedad de entero que especifica cuánto tiempo (en milisegundos) debe esperar el servidor para adquirir un bloqueo de escritura con el fin de confirmar una transacción. A menudo, es necesario un período de espera debido a que el servidor tiene que esperar a que se liberen otros bloqueos para poder establecer un bloqueo de escritura que confirme la transacción.  
  
 El valor predeterminado para esta propiedad es cero (0), lo que indica que el servidor esperará de forma indefinida. Para más información sobre las propiedades relacionadas con los bloqueos, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorBuildMaxThreads`  
 Propiedad de entero de 32 bits con signo que define el máximo de subprocesos asignados para generar índices de partición. Aumente este valor para acelerar la indización de particiones, a costa de usar memoria. Para obtener más información acerca de esta propiedad, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorCancelCount`  
 Una propiedad de entero de 32 bits con signo que define la frecuencia con la que el servidor debería comprobar si se ha producido un evento Cancel (según el recuento interno de iteraciones). Disminuya este número para comprobar Cancel más frecuentemente, a expensas del rendimiento general.  
  
 `CoordinatorCancelCount` se omite en modo de servidor tabular.  
  
 `CoordinatorExecutionMode`  
 Una propiedad de entero de 32 bits con signo que define el máximo de operaciones paralelas que intentará realizar el servidor, incluidas las operaciones de consulta y procesamiento. Cero (0) indica que el servidor decidirá, según un algoritmo interno. Un número positivo indica el máximo de operaciones en total. Un número negativo, con el signo invertido, indica el máximo de operaciones por procesador.  
  
 `CoordinatorExecutionMode` se omite en modo de servidor tabular.  
  
 El valor predeterminado para esta propiedad es -4, que indica que el servidor está limitado a 4 operaciones paralelas por procesador. Para obtener más información acerca de esta propiedad, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 `CoordinatorQueryMaxThreads`  
 Una propiedad de entero de 32 bits con signo que define el máximo de subprocesos por segmento de partición durante una resolución de consulta. Cuanto menor sea el número de usuarios simultáneos, mayor podrá ser este valor, a expensas de la memoria. Por el contrario, puede ser necesario disminuirlo si hay un gran número de usuarios simultáneos.  
  
 `CoordinatorShutdownMode`  
 Una propiedad booleana que define el modo de apagado del coordinador. Se trata de una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataDir`  
 Una propiedad de cadena que identifica el nombre del directorio en el que se almacenan los datos.  
  
 `DeploymentMode`  
 Determina el contexto operativo de una instancia de servidor de Analysis Services. Esta propiedad se denomina ‘modo de servidor’ en los cuadros de diálogo, los mensajes y la documentación. Esta propiedad la configura el programa de instalación de SQL Server en función del modo de servidor que se seleccione al instalar Analysis Services. Esta propiedad debe considerarse interna únicamente y siempre se usa el valor especificado por el programa de instalación.  
  
 Los valores válidos de esta propiedad incluyen los siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Este es el valor predeterminado. Especifica el modo multidimensional, utilizado para dar servicio a las bases de datos multidimensionales que usan el almacenamiento MOLAP, HOLAP y ROLAP, así como a los modelos de minería de datos.|  
|1|Especifica las instancias de Analysis Services que se instalaron como parte de una implementación de PowerPivot para SharePoint. No cambie la propiedad del modo de implementación de la instancia de Analysis Services que forma parte de una instalación de PowerPivot para SharePoint. Los datos PowerPivot dejarán de ejecutarse en el servidor si cambia el modo.|  
|2|Especifica el modo tabular empleado para hospedar las bases de datos de modelos tabulares que utilizan el almacenamiento en memoria o el almacenamiento DirectQuery.|  
  
 Cada modo excluye a los demás. Un servidor configurado para el modo tabular no podrá ejecutar las bases de datos de Analysis Services que contengan cubos y dimensiones. Si el hardware del equipo subyacente puede admitirlo, puede instalar varias instancias de Analysis Services en el mismo equipo y configurar cada instancia para utilizar otro modo. Recuerde que Analysis Services es una aplicación que usa muchos recursos. La implementación de varias instancias en el mismo sistema solo se recomienda para los servidores de tecnología avanzada.  
  
 `EnableFast1033Locale`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `ExternalCommandTimeout`  
 Propiedad de entero que define el tiempo de espera, en segundos, para comandos emitidos a servidores externos, incluidos los orígenes de datos relacionales y los servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] externos.  
  
 El valor predeterminado para esta propiedad es 3600 (segundos).  
  
 `ExternalConnectionTimeout`  
 Propiedad de entero que define el tiempo de espera, en segundos, para crear conexiones con servidores externos, incluidos los orígenes de datos relacionales y los servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] externos. Esta propiedad se omite si se especifica un tiempo de espera de conexión en la cadena de conexión.  
  
 El valor predeterminado para esta propiedad es 60 (segundos).  
  
 `ForceCommitTimeout`  
 Propiedad de entero que especifica cuánto tiempo, en milisegundos, debe esperar una operación de confirmación de escritura antes de cancelar otros comandos que preceden al comando actual, incluyendo las consultas en curso. Esto permite que la transacción de confirmación continúe y cancele las operaciones con una prioridad más baja, como las consultas.  
  
 El valor predeterminado de esta propiedad es 30 segundos (30000 milisegundos), lo que indica que otros comandos no se verán forzados a agotar su tiempo hasta que la transacción de confirmación haya esperado 30 segundos.  
  
> [!NOTE]  
>  Las consultas y procesos cancelados por este evento generarán el mensaje de error siguiente: "`Server: The operation has been cancelled`"  
  
 Para obtener más información acerca de esta propiedad, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
> [!IMPORTANT]  
>  `ForceCommitTimeout` se aplica a los comandos de procesamiento de cubos y las operaciones de reescritura.  
  
 `IdleConnectionTimeout`  
 Propiedad de entero que especifica un tiempo de espera, en segundos, para las conexiones que están inactivas.  
  
 El valor predeterminado para esta propiedad es cero (0), que indica que las conexiones inactivas no agotarán el tiempo de espera.  
  
 `IdleOrphanSessionTimeout`  
 Propiedad de entero que define, en segundos, cuánto tiempo se conservarán las sesiones huérfanas en la memoria del servidor. Una sesión huérfana es aquella que ya no tiene una conexión asociada. El valor predeterminado es 120 segundos.  
  
 `InstanceVisible`  
 Propiedad booleana que indica si la instancia del servidor está visible para detectar solicitudes de instancia del servicio SQL Server Browser. El valor predeterminado es True. Si lo establece en false, la instancia no está visible para SQL Server Browser.  
  
 `Language`  
 Propiedad de cadena que define el idioma, incluidos los mensajes de error y el formato de números. Esta propiedad invalida la propiedad CollationName.  
  
 El valor predeterminado para esta propiedad es en blanco, que indica que la propiedad CollationName define el idioma.  
  
 `LogDir`  
 Una propiedad de cadena que identifica el nombre del directorio que contiene los registros del servidor. Esta propiedad solo se aplica cuando se utilizan archivos de disco para realizar el registro, a diferencia de cuando se utilizan tablas de base de datos (comportamiento predeterminado).  
  
 `MaxIdleSessionTimeout`  
 Propiedad de entero que define el tiempo de espera máximo de una sesión inactiva, en segundos. El valor predeterminado es cero (0), lo que indica que nunca se agota el tiempo de espera de las sesiones. Sin embargo, las sesiones inactivas se quitarán si el servidor sufre restricciones de recursos.  
  
 `MinIdleSessionTimeout`  
 Propiedad de entero que define el tiempo mínimo, en segundos, que las sesiones inactivas tardarán en agotar el tiempo de espera. El valor predeterminado es 2700 segundos. Después de que expire este tiempo, el servidor puede finalizar la sesión inactiva, pero solo lo hará a medida que se necesite memoria.  
  
 `Port`  
 Propiedad de entero que define el número de puerto en el que el servidor escuchará las conexiones de los clientes. Si no está establecida, el servidor encontrará de forma dinámica el primer puerto no usado.  
  
 El valor predeterminado para esta propiedad es cero (0), que a su vez establece el valor predeterminado en el puerto 2383. Para obtener más información acerca de la configuración de puertos, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 `ServerTimeout`  
 Entero que define el tiempo de espera, en segundos, para las consultas. El valor predeterminado es de 3600 segundos (o 60 minutos). El valor cero (0) especifica que no se agotará el tiempo de espera de las consultas.  
  
 `TempDir`  
 Propiedad de cadena que especifica la ubicación de almacenamiento de los archivos temporales utilizados durante las operaciones de procesamiento y restauración, entre otras. El valor predeterminado de esta propiedad viene determinado por la configuración. Si no se especifica, el valor predeterminado es el directorio Data.  
  
## <a name="requestprioritization-category"></a>Categoría RequestPrioritization  
 `Enabled`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `StatisticsStoreSize`  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades del servidor en Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
