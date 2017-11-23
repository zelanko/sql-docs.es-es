---
title: "Actualizar los componentes de aprendizaje de máquina en una instancia de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: ea0784bc94dd3d3f4b7d11d83e92235591385396
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>Actualizar los componentes de aprendizaje de máquina en una instancia de SQL Server

Este artículo explica el proceso de _enlace_, que puede usar para actualizar los componentes que se usan en SQL Server de aprendizaje automático. El proceso de enlace bloquea el servidor a un ritmo de actualización basado en versiones de servidor de aprendizaje de máquina, en lugar de usar el servidor SQL Server de la versión y actualizar la programación.

> [!IMPORTANT]
> No es necesario utilizar el proceso de actualización si desea obtener las actualizaciones como parte de las actualizaciones de SQL Server. Siempre que se instala un nuevo service pack o una versión de servicio, componentes de aprendizaje de máquina se actualizan automáticamente siempre a la versión más reciente. Utilice únicamente la _enlace_ procesar si desea actualizar los componentes a un ritmo más rápido que concedidos por las versiones de servicio de SQL Server.

Si en cualquier momento en que desea detener la actualización en la programación del servidor de aprendizaje de máquina, debe _desenlace_ la instancia como se describe en [en esta sección](#bkmk_Unbind)y desinstalar el servidor de aprendizaje de máquina.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="binding-vs-upgrading"></a>Enlace frente a actualizar

El proceso de actualización de los componentes de aprendizaje automático se conoce como **enlace**, debido a que cambia el modelo de soporte técnico para componentes de aprendizaje de máquina de SQL Server usar la nueva directiva de ciclo de vida de Software modernas. 

En general, al cambiar al nuevo modelo de licencias se garantiza que los científicos de datos pueden usar siempre la versión más reciente de R o Python. Para obtener más información acerca de los términos de la directiva de ciclo de vida moderno, consulte [escala de tiempo del soporte técnico de Microsoft R Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support).

> [!NOTE]
> La actualización no cambia el modelo de compatibilidad para la base de datos de SQL Server y no cambia la versión de SQL Server.

Al enlazar una instancia, ocurren varias cosas:

+ Se cambia el modelo de soporte técnico. En lugar de confiar en las versiones de servicio de SQL Server, soporte técnico se basa en la nueva directiva de ciclo de vida moderna.
+ Los componentes de aprendizaje de máquina asociados a la instancia se actualizan automáticamente con cada versión, en el paso de bloqueo con la versión actual en la nueva directiva de ciclo de vida moderna. 
+ Pueden agregar nuevos paquetes de R o Python. Por ejemplo, las actualizaciones anteriores en función de Microsoft R Server 9.1 agregarán nuevos paquetes de R, como [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), y [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ La instancia ya no se puede actualizar manualmente, excepto para agregar paquetes nuevos.
+ Obtiene la opción para instalar previamente entrenados modelos proporcionados por Microsoft.

## <a name="bkmk_prereqs"></a>Prerequisites

Comience por identificar instancias que son candidatos para realizar una actualización. Si ejecuta el programa de instalación y seleccione la opción de enlace, devuelve una lista de instancias que son compatibles con la actualización.

Consulte la tabla siguiente para obtener una lista de actualizaciones admitidas y requisitos.

| Versión de SQL Server| Actualización compatible| Notas|
|-----|-----|------|
| SQL Server 2016| Servidor 9.2.1 de aprendizaje automático| Requiere al menos Service Pack 1 más CU3. R Services debe estar instalada y habilitada.|
| SQL Server 2017| Servidor 9.2.1 de aprendizaje automático| Servicios de aprendizaje de máquina (In-Database) debe estar instalados y habilitados. |

## <a name="bind-or-upgrade-an-instance"></a>Enlazar o actualizar una instancia

Aprendizaje de máquina Server para Windows incluye una herramienta que puede usar para actualizar los lenguajes y herramientas asociados a una instancia de SQL Server de aprendizaje automático. Hay dos versiones de la herramienta: un asistente y una utilidad de línea de comandos.

Antes de poder ejecutar el asistente o la herramienta de línea de comandos, debe descargar la versión más reciente del instalador independiente para componentes de aprendizaje automático.

+ [Instalar para Windows Server 9.2.1 de aprendizaje automático](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [Descargar los componentes necesarios para la instalación sin conexión](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>Actualizar mediante el Asistente para instalación nueva

1. Inicie al instalador de nuevo para el servidor de aprendizaje de máquina. Asegúrese de ejecutar el programa de instalación en el equipo que tiene la instancia que desea actualizar.

    ![Asistente para la instalación de servidor de aprendizaje de máquina de Microsoft](media/mls-921-installer-start.PNG)

2. En la página, **configurar la instalación**, confirme los componentes que desea actualizar y revisar la lista de instancias compatibles. Si no se muestra ninguna instancia, compruebe el [requisitos previos](#bkmk_prereqs).

    Para actualizar una instancia, seleccione la casilla de verificación situada junto al nombre de instancia. Si no selecciona una instancia, se crea una instalación independiente del servidor de aprendizaje de máquina y las bibliotecas de SQL Server son iguales.

    ![Asistente para la instalación de servidor de aprendizaje de máquina de Microsoft](media/configure-the-installation.PNG)

3. En el **del acuerdo de licencia** página, seleccione **acepto estos términos** para aceptar los términos de licencia para el servidor de aprendizaje de máquina. 

4. En las páginas sucesivas, dar su consentimiento a las condiciones de licencias adicionales para ningún componente de código abierto que ha seleccionado, como Microsoft R Open o la distribución de Anaconda de Python.

5. En el **casi** página, tome nota de la carpeta de instalación. La carpeta predeterminada es `~\Program Files\Microsoft\ML Server`.

    Si desea cambiar la carpeta de instalación, haga clic en **avanzadas** para volver a la primera página del asistente. Sin embargo, debe repetir todas las selecciones anteriores.

6. Si va a instalar los componentes sin conexión, puede se le pedirán la ubicación de los componentes de aprendizaje necesaria del equipo, como Microsoft R Open, servidor de Python y Python abierta.

Durante el proceso de instalación, se reemplazan las bibliotecas de R o Python utilizadas por SQL Server y Launchpad se actualiza para usar los componentes más recientes. Como resultado, si la instancia había utilizado previamente bibliotecas en la carpeta R_SERVICES de manera predeterminada, después de la actualización se quitan estas bibliotecas y se cambian las propiedades para el servicio Launchpad, para usar las bibliotecas en la nueva ubicación.

### <a name="bkmk_BindCmd"></a>Actualizar mediante la línea de comandos

Si no desea utilizar el asistente, puede instalar el servidor de aprendizaje de máquina y, a continuación, ejecutar la herramienta de SqlBindR.exe desde la línea de comandos para actualizar la instancia.

> [!TIP]
> 
> ¿No se puede encontrar SqlBindR.exe? Probablemente ha descargado los componentes enumerados anteriormente. Esta utilidad está disponible solo con el instalador de Windows para el servidor de aprendizaje de máquina.

1. Abra un símbolo del sistema como administrador y vaya hasta la carpeta que contiene sqlbindr.exe. La ubicación predeterminada es`C:\Program Files\Microsoft\MLServer\Setup`

2. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
  
   Anote el nombre completo de la instancia como se muestra. Por ejemplo, podría ser el nombre de instancia `MSSQL14.MSSQLSERVER` para una instancia predeterminada, o algo parecido a `SERVERNAME.MYNAMEDINSTANCE`.

3. Ejecute el **SqlBindR.exe** comando con el */enlazar* argumento y especifique el nombre de la instancia a actualizar, utilizando el nombre de instancia que se devuelve en el paso anterior.

   Por ejemplo, para actualizar la instancia predeterminada, escriba:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Una vez finalizada la actualización, reinicie el servicio de Launchpad asociado a cualquier instancia que se ha modificado.

## <a name="bkmk_Unbind"></a>Revertir o desenlazar una instancia

Si decide que ya no desea actualizar los componentes mediante el servidor de aprendizaje de máquina de aprendizaje automático, primero debe _desenlace_ la instancia y, a continuación, desinstalar el servidor de aprendizaje de máquina.

+ Desenlace la instancia

    Puede deshacer el enlace de la instancia y revertir a las bibliotecas originales instaladas por SQL Server, mediante cualquiera de estos dos métodos:

    + [Usar el Asistente para instalación](#bkmk_wizunbind) para servidor de aprendizaje de máquina y anule la selección de todas las características en la instancia
    + [Use la utilidad SqlBindR](#bkmk_cmdunbind) con el `/unbind` argumento, seguido del nombre de instancia.

    Una vez completado el proceso de separación, máquina futuras actualizaciones en función de servidor de aprendizaje de máquina de aprendizaje ya no se aplicarán a la instancia.

+ Desinstalar el servidor de aprendizaje automático

    Para obtener instrucciones, consulte [desinstalar máquina aprendizaje para Windows del servidor](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall). 

### <a name="bkmk_wizunbind"></a>Deshacer el enlace con el Asistente para

1. Busque el programa de instalación de servidor de aprendizaje de máquina. Si ha quitado el programa de instalación, tendrá que descargarlo de nuevo, o copiarlo desde otro equipo.
2. Asegúrese de ejecutar el programa de instalación en el equipo que tiene la instancia que desee separar.
2. El programa de instalación identifica las instancias locales que son candidatos para deshacer el enlace.
3. Anule la selección de la casilla de verificación situada junto a la instancia que se va a volver a la configuración original.
4. Acepte el contrato de licencia. Debe indicar su aceptación de términos de licencia incluso cuando se instala.
5. Haga clic en **Finalizar**. El proceso tarda algún tiempo.

### <a name="bkmk_cmdunbind"></a>Deshacer el enlace mediante la línea de comandos

1. Abra un símbolo del sistema y vaya a la carpeta que contiene **sqlbindr.exe**, como se describe en la sección anterior.

2. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia.

   Por ejemplo, el comando siguiente restablece la instancia predeterminada:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran problemas conocidos específicos para usar de la utilidad SqlBindR.exe o a las actualizaciones del servidor de aprendizaje de máquina que podrían afectar a instancias de SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando los paquetes que estaban previamente instalados

En la utilidad de actualización que se incluye con Microsoft R Server 9.0.1, la utilidad no restauró los paquetes originales o componentes de R completo, que requieren que el usuario ejecute la reparación en la instancia, aplican todas las versiones de servicio y, a continuación, reinicie la instancia.

Sin embargo, la versión más reciente de la utilidad actualización restaura automáticamente las características de R originales. Por lo tanto, no es necesario volver a instalar los componentes de R o volver a aplicar la revisión del servidor. Sin embargo, debe instalar los paquetes de R que pueden haber agregado tras la instalación inicial.

Si ha usado las funciones de administración de paquetes para instalar y compartir el paquete, esta tarea es mucho más fácil: puede usar comandos de R para sincronizar los paquetes instalados en el sistema de archivos con registros de la base de datos y viceversa. Para obtener más información, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas con varias actualizaciones de SQL Server

Si previamente ha actualizado una instancia de SQL Server 2016 R Services a 9.0.1, al ejecutar el nuevo instalador de Microsoft R Server 9.1.0, muestra una lista de todas las instancias válidas y, a continuación, de forma predeterminada, selecciona instancias enlazadas previamente. Si continúa, las instancias enlazadas previamente son independientes. Como resultado, el 9.0.1 anteriores se quita la instalación, los incluidos relacionados con los paquetes, pero no se instala la nueva versión de Microsoft R Server (9.1.0).

Como alternativa, puede modificar la instalación del servidor de R existente como se indica a continuación:
1. En el Panel de Control, abra **agregar o quitar programas**.
2. Busque Microsoft R Server y haga clic en **cambiar o modificar**.
3. Cuando se inicia el programa de instalación, seleccione las instancias que desea enlazar a 9.1.0.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Enlazar o desenlazar deja varias carpetas temporales

A veces, el enlace y operaciones Desenlazando producirá un error limpiar las carpetas temporales.
Si encuentra carpetas con un nombre parecido a esto, puede quitarlo una vez completada la instalación:`R_SERVICES_<guid>`

> [!NOTE]
> Asegúrese de esperar hasta que finalice la instalación. Puede tardar mucho tiempo para quitar las bibliotecas de R asociadas con una versión y, a continuación, agregar las nuevas bibliotecas de R. Cuando se complete la operación, se quitan las carpetas temporales.

## <a name="sqlbindrexe-command-syntax"></a>Sintaxis de comandos de sqlbindr.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parámetros

|Nombre|Description|
|------|------|
|*list*| Muestra una lista de todos los identificadores de instancia de SQL Database en el equipo actual.|
|*bind*| Actualiza la instancia de SQL Database especificada a la versión más reciente de R Server y garantiza que la instancia obtenga automáticamente las actualizaciones futuras de R Server.|
|*unbind*|Desinstala la versión más reciente de R Server de la instancia de SQL Database especificada e impide que las actualizaciones futuras de R Server afecten a la instancia.|

### <a name="errors"></a>Errores

La herramienta devuelve los siguientes mensajes de error:

|Error|Solución|
|------|------|
|An error occurred while binding the instance (Se produjo un error al enlazar la instancia)| No se pudo enlazar la instancia. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.|
|The instance is already bound (La instancia ya está enlazada)| Ha ejecutado el comando *bind* , pero la instancia especificada ya está enlazada. Elija una instancia diferente.|
|The instance is not bound (La instancia no está enlazada)| Ha ejecutado el comando *unbind* , pero la instancia especificada no está enlazada. Elija una instancia diferente que sea compatible.|
|Not a valid SQL instance ID (Identificador de instancia de SQL no válido)| Puede que haya escrito el nombre de instancia incorrectamente. Ejecute el comando de nuevo con el argumento *list* para ver los identificadores de instancia disponibles.|
|No se encontraron instancias| Este equipo no tiene una instancia de SQL Server R Services.|
|La instancia debe tener instalada una versión compatible de SQL R Services (en bases de datos).| Vea los requisitos de compatibilidad de este tema para obtener más información.|
|An error occurred while unbinding the instance (Se produjo un error al desenlazar la instancia)| No se pudo desenlazar la instancia. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.|
|Error inesperado| Otros errores. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.  |
|No SQL instances found (No se encontraron instancias de SQL)| Este equipo no tiene una instancia de SQL Server. |

Para obtener más información, vea las notas de la versión para Microsoft R Server:

+ [Problemas conocidos en el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [Anuncios de características de la versión anterior del servidor de R](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [Características desusadas, discontinuos o modificadas](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
