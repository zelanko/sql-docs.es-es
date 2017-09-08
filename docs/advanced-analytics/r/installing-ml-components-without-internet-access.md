---
title: "Instalar componentes sin acceso a Internet de aprendizaje automático | Documentos de Microsoft"
ms.custom: 
ms.date: 04/20/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7307104b9ad5df2bb8f034525cc82847d21a14bf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>Instalar componentes sin acceso a Internet de aprendizaje automático

Dado que los componentes de R y Python suministrados con SQL Server 2016 o SQL Server 2017 son código abierto, Microsoft no instala los componentes de R o Python de forma predeterminada.

En su lugar, se proporcionan a los instaladores relacionados e incluirse paquetes como una comodidad en Microsoft Download Center y otros sitios de confianza. Debe dar su consentimiento a la licencia apropiada y, a continuación, el programa de instalación de SQL Server instalará los componentes de R o Python para usted.

Este tema proporciona las ubicaciones de descarga para los instaladores y una visión general del proceso de instalación sin conexión.

## <a name="installation-process"></a>Proceso de instalación

Normalmente, el programa de instalación de los componentes de máquina usado en SQL Server 2016 y SQL Server 2017 requiere una conexión a Internet. Cuando se ejecuta el programa de instalación de SQL Server, si ha seleccionado una de las opciones de learnig de máquina, el programa de instalación comprobará la Python o R instaladores, como así como cualquier otras componentes necesarios. Si hay una conexión a Internet, SQL Server instalará automáticamente.

> [!IMPORTANT]
> En un servidor sin acceso a Internet, debe descargar a los instaladores adicionales antes de continuar con el programa de instalación.

Como mínimo, debe descargar a los instaladores de R o Python que son compatibles con la versión o el número de compilación de SQL Server que va a instalar.

Dependiendo de la configuración del servidor, puede que tenga componentes adicionales, como .NET Core.  Vea [componentes adicionales](#bkmk_OtherComponents) para obtener más información.

Después de haber descargado a los instaladores, usa al instalar la característica como parte del programa de instalación de SQL Server.

### <a name="step-1-obtain-additional-installers"></a>Paso 1. Obtener a instaladores adicionales

Para **R** en SQL Server 2016 y 2017 de SQL Server, debe obtener dos instaladores diferentes. El Asistente para la instalación de SQL Server se asegurará de que se instalen en el orden correcto.

+ Instaladores con **SRO** en el nombre proporcionan los componentes de código abierto.
+ Insallers con **SRS** en el nombre contienen componentes proporcionados por Microsoft, los de integración de base de datos incluidos.


Para **Python** en SQL Server 2017, descargue el archivo CAB único y los requisitos previos.


1. Descargue los instaladores de los [sitios del Centro de descarga de Microsoft](#installerlocs) en un equipo con acceso a Internet y guarde el instalador (en lugar de ejecutarlo).
2. Copie los archivos del instalador (CAB) en el equipo donde vaya a instalar componentes de aprendizaje de máquina.
3. Actualmente, el Asistente para instalación instala a inglés de forma predeterminada. Para instalar un idioma diferente, modifique los nombres de archivo de instalador como se describe aquí: [modificaciones necesarias para diferentes configuraciones regionales de idioma](#modslocales).
4. Descargar los componentes adicionales que son necesarios, como MPI o .NET Core.
5. Si lo desea, puede descargar el código fuente archivado de los componentes de código abierto, pero esto no es necesario para el programa de instalación de SQL Server y se puede realizar en cualquier momento. Para obtener más información, consulte [R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).


> [!NOTE]
> Asegúrese de obtener los archivos que coincidan con la versión de SQL Server que va a instalar.
> 
> Se proporciona soporte técnico para Python en SQL Server de 2017 CTP 2.0. Las versiones anteriores, incluidos SQL Server 2016, no son compatibles con Python.

Para ver un tutorial paso a paso del proceso de instalación sin conexión para R Services en SQL Server 2016, se recomienda artículo por la [al equipo de asesoramiento al cliente SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/). También se abordan escenarios de instalación integrada y aplicación de revisiones.


### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>Paso 2. Ejecute el programa de instalación sin conexión mediante el Asistente para la instalación de SQL Server

1. Ejecute el Asistente para la instalación de SQL Server.
2. Cuando el Asistente para instalación muestra la página de licencia, haga clic en **Accept**.
3. Aparece un cuadro de diálogo que solicita la **ruta de instalación** de los paquetes necesarios.
4. Haga clic en **examinar** para buscar la carpeta que contiene los archivos de instalador que copió anteriormente.
5. Si encuentra los archivos correctos, haga clic en **Siguiente** para indicar que los componentes están disponibles.
10. Complete el Asistente para la instalación de SQL Server.
11. Realice los pasos posteriores a la instalación necesarios para asegurarse de que el servicio está habilitado.

## <a name="installerlocs"></a>Descargas

Versión  |Vínculo de descarga  
---------|---------
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
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 GDR**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**2017 CTP 1 de SQL Server**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**Versión de CTP de SQL Server de 2017 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**Versión de CTP de SQL Server de 2017 1.4** |
Microsoft R Open     |[SRO_xxxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_xxx.xxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server de 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Abra Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Servidor de Python de Microsoft    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)

Si desea ver el código fuente de Microsoft R, está disponible para su descarga como un archivo en formato de .tar: [instaladores descargar R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download)

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

Si descarga los archivos .cab como parte de la instalación de SQL Server en un equipo con acceso a Internet, el Asistente para la instalación detectará el idioma local y cambiará automáticamente el idioma del instalador.

Pero si está instalando una de las versiones localizadas de SQL Server en un equipo sin acceso a Internet y descarga los instaladores de R en un recurso compartido local, deberá editar manualmente el nombre de los archivos descargados e insertar el identificador de idioma correcto del idioma que va a instalar.

Por ejemplo, si va a instalar la versión en japonés de SQL Server, deberá cambiar el nombre del archivo de SRS_8.0.3.0_**1033**.cab a SRS_8.0.3.0_**1041**.cab.


## <a name="slipstream-upgrades"></a>Actualizaciones de instalación integrada

Por instalación integrada se entiende la capacidad de aplicar una revisión o actualización a una instalación de instancia con errores con el propósito de reparar problemas existentes. La ventaja de este método es que el servidor SQL Server se actualiza al mismo tiempo que se realiza la instalación, lo que evita un reinicio independiente más adelante.

+ Si el servidor no tiene acceso a Internet, debe descargar el instalador de SQL Server y, seguidamente, descargar las versiones de los instaladores de componentes R que corresponda **antes de** comenzar el proceso de actualización.  Los componentes de R no se incluyen de forma predeterminada con SQL Server.

+ Si está *agregar* estos componentes a un *existente* instalación, utilice la versión actualizada del instalador de SQL Server y la correspondiente versión actualizada de los componentes adicionales. Cuando se especifica que la característica de R es esté instalado, el programa de instalación buscará la versión correspondiente de los instaladores para los componentes de aprendizaje automático.

## <a name="command-line-arguments-for-setup"></a>Argumentos de línea de comandos para el programa de instalación

Al realizar una instalación desatendida, debe proporcionar los siguientes argumentos de línea de comandos. Tenga en cuenta que no es necesario establecer las marcas adicionales para instalar más componentes necesarios. Requisitos previos como .NET core se instalan automáticamente de forma predeterminada.

**Ubicación de instaladores**

- `/UPDATESOURCE`para especificar la ubicación del archivo local que contiene el programa de instalación de actualización de SQL Server
- `/MRCACHEDIRECTORY`para especificar la carpeta que contiene los archivos CAB de componentes de R

**Componentes de R en SQL Server 2016**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/IACCEPTROPENLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente

**Componentes de R en SQL Server SQL Server 2017**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/SQL_INST_MR`usar R
- `/IACCEPTROPENLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente

**Componentes de Python en SQL Server 2017**

- `/ADVANCEDANALYTICS`Para obtener compatibilidad con el motor de scripts externos
- `/SQL_INST_MPY`Para usar Python
- `/IACCEPTPYTHONLICENSETERMS="True"`para aceptar el contrato de licencia de R independiente

> [!TIP]
> En este artículo, el equipo de soporte técnico de servicios de R muestra cómo realizar una instalación desatendida o la actualización de servicios de R en SQL Server 2016: [implementar R Services en equipos sin acceso a Internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

## <a name="see-also"></a>Vea también

[Instalar Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)


