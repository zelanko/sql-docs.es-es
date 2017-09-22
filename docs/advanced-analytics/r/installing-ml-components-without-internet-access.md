---
title: "Instalación de componentes de aprendizaje de máquina sin acceso a internet | Documentos de Microsoft"
ms.custom: 
ms.date: 09/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f684f0168e57c5cd727af6488b2460eeaead100c
ms.openlocfilehash: 1facfc7a52aa9e98aacc6c6d059acf8823e86170
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>Instalación de componentes de aprendizaje de máquina sin acceso a internet

Dado que los componentes de R y Python proporcionados con SQL Server 2016 y SQL Server 2017 son código abierto, Microsoft no instala los componentes de R o Python de forma predeterminada.

En su lugar, se proporcionan a los instaladores relacionados e incluirse paquetes como una comodidad en Microsoft Download Center y otros sitios de confianza. Debe dar su consentimiento a la licencia apropiada y, a continuación, el programa de instalación de SQL Server instala los componentes de R o Python.

Este tema proporciona las ubicaciones de descarga para los instaladores y una visión general del proceso de instalación sin conexión.

## <a name="installation-process"></a>Proceso de instalación

Normalmente, el programa de instalación de los componentes de máquina usado en SQL Server 2016 y SQL Server 2017 requiere una conexión a internet. Cuando se ejecuta el programa de instalación de SQL Server, si ha seleccionado alguna del opciones de aprendizaje automático, el programa de instalación comprueba la Python o R instaladores, como así como cualquier otras componentes necesarios.

+ **Si el equipo tiene una conexión a internet**

    SQL Server busca y descargar los componentes para, a continuación, se instala durante la instalación. Debe aceptar los términos de licencia por separado para cada componente de código abierto (R o Python) que se instala.

+ **Si el equipo no tiene acceso a internet**

    Debe descargar a los instaladores adicionales antes de continuar con el programa de instalación. Como mínimo, descargue a los instaladores de R o Python que son compatibles con la versión de SQL Server que va a instalar.

    Dependiendo de la configuración del servidor, puede que tenga componentes adicionales.  Vea [componentes adicionales](#bkmk_OtherComponents) para obtener más información.

    Después de haber descargado a los instaladores, usa al instalar la característica como parte del programa de instalación de SQL Server.

### <a name="step-1-obtain-additional-installers"></a>Paso 1. Obtener a instaladores adicionales

Para **R** en SQL Server 2016 y 2017 de SQL Server, debe obtener dos instaladores diferentes. El Asistente para la instalación de SQL Server se asegura de que se instalan en el orden correcto.

+ Instaladores con **SRO** en el nombre proporcionan los componentes de código abierto.
+ Instaladores con **SRS** en el nombre contienen componentes proporcionados por Microsoft, los de integración de base de datos incluidos.

Para **Python** en SQL Server 2017, descargue el archivo CAB único y los requisitos previos.

1. Descargar los instaladores de la [sitios de Microsoft Download Center](#installerlocs) en un equipo con acceso a internet y guarde el programa de instalación en lugar de ejecutarlo.
2. Copie los archivos del instalador (CAB) en el equipo donde desea instalar los componentes de aprendizaje de máquina.
3. SQL Server 2016, el Asistente para instalación instala a inglés de forma predeterminada. Para instalar un idioma diferente necesarias modificación del nombre de archivo instalador, como se describe aquí: [las modificaciones necesarias para las diferentes configuraciones regionales](#modslocales).
    Para SQL Server 2017, se identifica el idioma correcto según la configuración regional de la instancia.
4. Descargar los componentes adicionales que son necesarios, como MPI o .NET Core.
5. Si lo desea, puede descargar el código fuente archivado de los componentes de código abierto, pero esto no es necesario para el programa de instalación de SQL Server y se puede realizar en cualquier momento. Para obtener más información, consulte [R Server para Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows).

Para ver un tutorial paso a paso del proceso de instalación sin conexión para R Services en SQL Server 2016, se recomienda artículo por la [al equipo de asesoramiento al cliente SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). el artículo incluye capturas de pantalla y también cubre los escenarios de instalación de aplicación de revisiones y la instalación integrada.

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Paso 2. Ejecute el programa de instalación sin conexión mediante el Asistente para la instalación de SQL Server

1. Ejecute el Asistente para la instalación de SQL Server.
2. Cuando el Asistente para instalación muestra la página de licencia, haga clic en **Accept**.
3. Aparece un cuadro de diálogo que solicita la **ruta de instalación** de los paquetes necesarios.
4. Haga clic en **examinar** para buscar la carpeta que contiene los archivos de instalador que copió anteriormente.
5. Si encuentra los archivos correctos, haga clic en **Siguiente** para indicar que los componentes están disponibles.
10. Complete el Asistente para la instalación de SQL Server.
11. Realice los pasos posteriores a la instalación necesarios para asegurarse de que el servicio está habilitado.

## <a name="installerlocs"></a>Dónde descargar componentes de aprendizaje de máquina

> [!NOTE]
> Asegúrese de obtener los archivos que coinciden con la versión de SQL Server que se va a instalar.
> 
> Se proporciona soporte para Python a partir de SQL Server de 2017 CTP 2.0. Las versiones anteriores, incluidos SQL Server 2016, no son compatibles con Python.

+ [Para obtener los componentes de R para SQL Server 2016](#bkmk_2016Installers)

+ [Para obtener los componentes de R o Python para SQL Server 2017](#bkmk_2017Installers)

### <a name="bkmk_2017Installers"></a>Descargas para SQL Server de 2017

Versión  |Vínculo de descarga  |
---------|---------|
**2017 CTP 1 de SQL Server**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**Versión de CTP de SQL Server de 2017 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**Versión de CTP de SQL Server de 2017 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server de 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Abra Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Servidor de Python de Microsoft    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**2017 CTP 3.0 de SQL Server** |
Microsoft R Open     |sin cambios; usar CTP 2.0|
Microsoft R Server     |sin cambios; usar CTP 2.0|
Abra Microsoft Python     |sin cambios; usar CTP 2.0|
Servidor de Python de Microsoft    |sin cambios; usar CTP 2.0|
**Versión de CTP de SQL Server de 2017 4.0** |
Microsoft R Open     |sin cambios; usar CTP 2.0|
Microsoft R Server     |sin cambios; usar CTP 2.0|
Abra Microsoft Python     |sin cambios; usar CTP 2.0|
Servidor de Python de Microsoft    |sin cambios; usar CTP 2.0|
**RTM de SQL Server de 2017** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Abra Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Servidor de Python de Microsoft    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

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

Si desea ver el código fuente de Microsoft R, está disponible para su descarga como un archivo en formato de .tar: [instaladores descargar R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>Requisitos previos adicionales

Dependiendo del entorno, deberá realizar copias locales de los instaladores en relación con los siguientes requisitos previos.

Componente  |Versión
---------|---------
[Proveedor OLE DB de Microsoft AS para SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0


## <a name="modslocales"></a>Instalar para diferentes idiomas.

Si descargó el. Archivos CAB como parte del programa de instalación de SQL Server en un equipo con acceso a internet, el Asistente para instalación se detecta el idioma local y se cambia automáticamente el idioma del instalador.

Sin embargo, dependiendo de la versión de SQL Server, deberá realizar pasos adicionales para instalar los componentes de R localizados en un equipo sin acceso a internet.

+ **Para SQL Server 2016**

   Después de descargar a los instaladores de R en un recurso compartido local, debe editar manualmente el nombre de los archivos descargados para insertar el identificador de idioma correcto para el idioma que se va a instalar.

    Por ejemplo, para instalar la versión en japonés de SQL Server, cambiaría el nombre del archivo de SRS_8.0.3.0_**1033**.cab a SRS_8.0.3.0_**1041**.cab.

    > [!IMPORTANT]
    > Este problema aplica a las versiones anteriores sólo a y se ha solucionado en versiones posteriores.
    > Utilice esta solución solamente si el programa de instalación devuelve un mensaje que no se puede instalar el idioma correcto.

+ **Para SQL Server de 2017**

    Descargue la. Archivo .cab para los componentes de R o Python.
    
    Se detecta el idioma en función de la configuración regional del servidor. La configuración regional correcta se instala automáticamente con descargado. Archivo CAB.

## <a name="slipstream-upgrades"></a>Actualizaciones de instalación integrada

Por instalación integrada se entiende la capacidad de aplicar una revisión o actualización a una instalación de instancia con errores con el propósito de reparar problemas existentes. La ventaja de este método es que el servidor SQL Server se actualiza al mismo tiempo que se realiza la instalación, lo que evita un reinicio independiente más adelante.

+ Si el servidor no tiene acceso a Internet, debe descargar el instalador de SQL Server y, seguidamente, descargar las versiones de los instaladores de componentes R que corresponda **antes de** comenzar el proceso de actualización.  Los componentes de R no se incluyen de forma predeterminada con SQL Server.

+ Si está *agregar* estos componentes a un *existente* instalación, utilice la versión actualizada del instalador de SQL Server y la correspondiente versión actualizada de los componentes adicionales. Cuando se especifica que la característica de R es esté instalado, el programa de instalación busca la versión correspondiente de los instaladores para los componentes de aprendizaje automático.

## <a name="command-line-arguments-for-setup"></a>Argumentos de línea de comandos para el programa de instalación

Al realizar una instalación desatendida, debe proporcionar los siguientes argumentos de línea de comandos. Sin embargo, no es necesario establecer las marcas adicionales para instalar los componentes adicionales necesarios; requisitos previos como .NET core se instalan automáticamente de forma predeterminada.

**Ubicación de instaladores**

- `/UPDATESOURCE`para especificar la ubicación del archivo local que contiene el programa de instalación de actualización de SQL Server
- `/MRCACHEDIRECTORY`para especificar la carpeta que contiene los archivos CAB de componentes de R

**Componentes de R en SQL Server 2016**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/IACCEPTROPENLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente

**Componentes de R en SQL Server 2017**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/SQL_INST_MR`usar R
- `/IACCEPTROPENLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente

**Componentes de Python en SQL Server 2017**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/SQL_INST_MPY`Para usar Python
- `/IACCEPTPYTHONLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente


> [!NOTE]
> No se puede cambiar la cuenta de servicio para Launchpad con parámetros en el programa de instalación de SQL Server. Se recomienda que instale con las cuentas de servicio predeterminadas y, a continuación, modificar la cuenta de servicio mediante el Administrador de configuración de SQL Server. Una vez hecho esto, asegúrese de reiniciar el servicio Launchpad.

## <a name="see-also"></a>Vea también

[Instalar Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

En este artículo, el equipo de soporte técnico de servicios de R muestra cómo realizar una instalación desatendida o la actualización de servicios de R en SQL Server 2016: [implementar R Services en equipos sin acceso a Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).
