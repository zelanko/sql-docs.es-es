---
title: Instalar componentes de aprendizaje automático de SQL Server sin acceso a internet | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 289f304cf445882981fb110e9c00a395cac90e5f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585617"
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>Instalar componentes sin acceso a internet de aprendizaje de automático de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

De forma predeterminada, instaladores de conectan a sitios de descarga de Microsoft para obtener necesarios y componentes actualizados para equipo aprendizaje de SQL Server. Si hay restricciones de firewall impiden que el instalador alcanzar estos sitios, puede usar un dispositivo conectado a internet para descargar archivos, transferir archivos a un servidor sin conexión y, a continuación, ejecute el programa de instalación.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Requisito de instalación de revisión 

Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  


## <a name="download-cab-files"></a>Descargar archivos .cab

En un servidor conectado a internet, descargue los archivos .cab necesarios para una instalación sin conexión. El programa de instalación utiliza los archivos .cab para instalar características adicionales.

Versión  |Vínculo de descarga  |
---------|---------|
**Versión inicial de SQL Server 2017** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Abra Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Servidor de Python de Microsoft    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server de 2017 CU1** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Abra Microsoft Python     |sin cambios; Use anterior |
Servidor de Python de Microsoft    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server de 2017 CU2** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |sin cambios; Use anterior|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |sin cambios; Use anterior|
**SQL Server de 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server de 2017 CU4** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**SQL Server de 2017 CU5** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)|
**SQL Server de 2017 CU6** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)|
**SQL Server de 2017 CU7** |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server      |cambio o; Use anterior|
Abra Microsoft Python     |sin cambios; Use anterior|
Servidor de Python de Microsoft    |sin cambios; Use anterior|


### <a name="bkmk_2016Installers"></a>Descargas de SQL Server 2016

> [!IMPORTANT]
> 
> Al instalar SQL Server 2016 SP1 CU4 o CU5 SP1 sin conexión, descargue SRO_3.2.2.16000_1033.cab. Si ha descargado SRO_3.2.2.13000_1033.cab de FWLINK 831785 como se indica en el cuadro de diálogo de instalación, cambie el nombre del archivo como SRO_3.2.2.16000_1033.cab antes de instalar la actualización acumulativa.

Versión  |Vínculo de descarga  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     | sin cambios; Use anterior |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     |sin cambios; Use anterior|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     |sin cambios; Use anterior |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     |sin cambios; Use anterior|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 Service Pack 1 CU3**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server     |sin cambios; Use anterior|
**GDR y SQL Server 2016 SP 1 CU4**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |sin cambios; Use anterior|
Microsoft R Server    |sin cambios; Use anterior |

Si desea ver el código fuente de Microsoft R, está disponible para su descarga como un archivo en formato de .tar: [instaladores descargar R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Requisitos previos adicionales

Dependiendo del entorno, deberá realizar copias locales de los instaladores en relación con los siguientes requisitos previos.

Componente  |Versión
---------|---------
[Proveedor OLE DB de Microsoft AS para SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="transfer-files"></a>Transferencia de archivos

Transferir el disco de instalación de SQL Server comprimido y los archivos que ya ha descargado en el equipo en el que va a instalar el programa de instalación.

Colocar los archivos CAB en una carpeta adecuada como **descarga** o una carpeta temporal del usuario el programa de instalación: C:\Users < nombre de usuario > \AppData\Local\Temp.

Coloque el archivo en_sql_server_2017.iso en la carpeta apropiada. Haga doble clic en **setup.exe** para comenzar la instalación.

### <a name="run-setup"></a>Ejecute el programa de instalación

Al ejecutar el programa de instalación de SQL Server en un equipo desconectado de internet, el programa de instalación agrega un **instalación sin conexión** paginar en el Asistente para que pueda especificar la ubicación de los archivos .cab que copió en el paso anterior.

1. Inicie al Asistente para la instalación de SQL Server.

2. Cuando el Asistente para instalación muestra la página licencias de código abierto R o componentes de Python, haga clic en **Accept**. Aceptación de términos de licencia le permite continuar con el paso siguiente.

3. En el **instalación sin conexión** página **ruta de instalación**, especifique la carpeta que contiene los archivos .cab que copió anteriormente.

4. Continuar siguientes las indicaciones en pantalla para completar la instalación.

Una vez finalizada la instalación, reinicie el servicio y, a continuación, configurar el servidor para habilitar la ejecución de secuencias de comandos como se describe en [instalar SQL Server de 2017 Machine Learning Services (In-Database)](sql-machine-learning-services-windows-install.md) o [instalar SQL Server 2016 R Services (en bases de datos)](sql-r-services-windows-install.md).

## <a name="slipstream-upgrades-for-offline-servers"></a>Actualizaciones de instalación integrada para los servidores sin conexión

Por instalación integrada se entiende la capacidad de aplicar una revisión o actualización a una instalación de instancia con errores con el propósito de reparar problemas existentes. La ventaja de este método es que el servidor SQL Server se actualiza al mismo tiempo que se realiza la instalación, lo que evita un reinicio independiente más adelante.

+ Si el servidor no tiene acceso a Internet, debe descargar el instalador de SQL Server y, seguidamente, descargar las versiones de los instaladores de componentes R que corresponda **antes de** comenzar el proceso de actualización.  Los componentes de R no se incluyen de forma predeterminada con SQL Server.

+ Si va a agregar estos componentes a una instalación existente, use la versión actualizada del instalador de SQL Server y la correspondiente versión actualizada de los componentes adicionales. Cuando se especifica que la característica de R es esté instalado, el programa de instalación busca la versión correspondiente de los instaladores para los componentes de aprendizaje automático.

## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o actualización? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

En este artículo, el equipo de soporte técnico de servicios de R muestra cómo realizar una instalación desatendida o la actualización de servicios de R en SQL Server 2016: [implementar R Services en equipos sin acceso a Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).


## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).

