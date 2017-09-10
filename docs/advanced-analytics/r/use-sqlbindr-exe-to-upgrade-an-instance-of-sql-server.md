---
title: "Actualizar los componentes de aprendizaje de máquina en una instancia de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>Actualizar los componentes de aprendizaje de máquina en una instancia de SQL Server

Servidor de aprendizaje de máquina Microsoft para Windows incluye una herramienta que puede usar para actualizar los componentes de R asociados con una instancia de SQL Server. Hay dos versiones de la herramienta: un asistente y una utilidad de línea de comandos.

Este artículo describe cómo usar estas herramientas para actualizar una instancia compatible de SQL Server y cómo revertir una instancia que ya se había actualizada.

No es necesario utilizar el proceso de actualización si desea obtener las actualizaciones como parte de las actualizaciones de SQL Server. Siempre que se instala un nuevo service pack o una versión de servicio, componentes de aprendizaje de máquina se actualizan automáticamente siempre a la versión más reciente. Solo puede usar a este proess si desea actualizar los componentes a un ritmo más rápido que es affored por las versiones de servicio de SQL Server.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

> [!NOTE]
> En el momento de redactar este artículo, las actualizaciones se aplican únicamente a las instancias de SQL Server 2016 compatibles.  Aunque se admite la actualización de SQL Server 2017, no se ha publicado una nueva versión del servidor de aprendizaje de máquina de Microsoft que se usará para las actualizaciones.

## <a name="upgrade-an-instance"></a>Actualizar una instancia

El proceso de actualización se conoce como **enlace**, debido a que cambia el modelo de soporte técnico para los componentes de aprendizaje de máquina de SQL Server usar la nueva directiva de ciclo de vida moderna. Sin embargo, la actualización no cambia el modelo de compatibilidad para la base de datos de SQL Server.

En general, este sistema de licencias garantiza que los científicos de datos siempre usen la versión más reciente de R. Para más información sobre los términos y las ventajas de la directiva de ciclo de vida moderno, vea [Support Timeline for Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support) (Escala de tiempo de compatibilidad de Microsoft R Server).

Al enlazar una instancia, ocurren varias cosas:

+ Se cambia el modelo de soporte técnico. En lugar de confiar en las versiones de servicio de SQL Server, soporte técnico se basa en la nueva directiva de ciclo de vida moderna.
+ Los componentes asociados con la instancia de aprendizaje automático se actualizará automáticamente con cada versión, en el paso de bloqueo con la versión actual en la nueva directiva de ciclo de vida moderna. 
+ Pueden agregar nuevos paquetes de R o Python. Por ejemplo, las actualizaciones anteriores de Microsoft R Server agregan nuevos paquetes de R, como [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), y [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ La instancia ya no se puede actualizar manualmente, excepto para agregar paquetes nuevos.
+ Tiene la opción para agregar modelos previamente entrenados.

Si más adelante decide que desea detener la actualización de la instancia en cada versión, debe **desenlace** la instancia como se describe en [en esta sección](#bkmk_Unbind)y, a continuación, desinstale el equipo las actualizaciones de aprendizaje, tal como se describe en este artículo: [ejecutar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). Una vez completado el proceso, máquina futuras actualizaciones en función de servidor de aprendizaje de máquina de aprendizaje ya no se aplicarán a la instancia.

### <a name="bkmk_prereqs"></a>Requisitos previos para la actualización

1. Identificar las instancias que son candidatas para la actualización.
    + SQL Server 2016 con R Services instalado
    + CU3 además de al menos a Service Pack 1

2. Obtener **Microsoft R Server**, al descargar el instalador independiente de Windows.

    [Cómo instalar R Server 9.0.1 en Windows mediante el instalador independiente de Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)

> [!TIP]
> 
> ¿No se puede encontrar SqlBindR.exe? Probablemente no ha descargado R Server todavía. Esta utilidad está disponible solo con el instalador de Windows para Microsoft R Server.

### <a name="bkmk_BindWizard"></a>Actualizar mediante el Asistente para instalación nueva

1. Inicie al instalador de nuevo para el servidor de R en el equipo que tiene la instancia que desea actualizar.
  ![Asistente para la instalación de Microsoft R Server](media/r-server-installer-01.PNG)
2. Acepte el contrato de licencia para Microsoft R Server 9.1.0 y haga clic en **siguiente**.
3. Acepte las condiciones de licencias para los componentes de código abierto de R y haga clic en **siguiente**.
4. En **seleccionar la carpeta de instalación**, acepte los valores predeterminados o especificar una ubicación diferente donde se instalará bibliotecas de R. 
5. El instalador identificará todas las instancias locales que son candidatos para el enlace. Si no aparece ninguna instancia, significa que no se encuentra ninguna instancia válida. Deberá aplicar la revisión del servidor, o bien compruebe si se instaló R Services.
6. Active la casilla situada junto a cualquier instancia que se va a actualizar y haga clic en **siguiente**.
7. El proceso puede tardar unos instantes.
    
    Durante la instalación, SQL Server R Services utilizadas las bibliotecas de R se reemplazan con las bibliotecas de Microsoft R Server 9.1.0.
    
    LaunchPad no se ve afectado por el proceso, pero se quitarán las bibliotecas en la carpeta R_SERVICES y no se cambiarán las propiedades para el servicio, para usar las bibliotecas en `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="bkmk_BindCmd"></a>Actualizar mediante la línea de comandos

Después de haber instalado Microsoft R Server, puede ejecutar la herramienta de SqlBindR.exe desde la línea de comandos.

1. Abra un símbolo del sistema como administrador y vaya hasta la carpeta que contiene sqlbindr.exe. La ubicación predeterminada es`C:\Program Files\Microsoft\R Server\Setup`
2. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
  
   Anote el nombre completo de la instancia como se muestra. Por ejemplo, podría ser el nombre de instancia `MSSQL13.MSSQLSERVER` para la instancia predeterminada, o algo parecido a `SERVERNAME.MYNAMEDINSTANCE`.
3. Ejecute el comando **SqlBindR.exe** con el argumento */bind* y especifique el nombre de la instancia que se va a actualizar, como se devolvió en el paso anterior.

   Por ejemplo, para actualizar la instancia predeterminada, escriba:`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. Cuando finalice la actualización, reinicie el servicio Launchpad asociado a cualquier instancia que se haya modificado.


## <a name="bkmk_Unbind"></a>Revertir o desenlazar una instancia

Para restaurar una instancia de SQL Server para usar las bibliotecas originales instaladas por SQL Server, debe realizar una **desenlace** operación. Para ello, volviendo a ejecutar el Asistente para la instalación de Microsoft R Server, o si se ejecuta la utilidad SqlBindR desde la línea de comandos.

Cuando se desenlaza complete, se quitan las bibliotecas de Microsoft R Server 9.1.0 y se restauran las bibliotecas de R originales utilizadas por SQL Server R Services.

Se editan las propiedades de SQL Server Launchpad para usar las bibliotecas de R en la carpeta predeterminada para R_SERVICES, en `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="unbind-using-the-wizard"></a>Deshacer el enlace con el Asistente para

1. Descargar al nuevo instalador de Microsoft R Server 9.1.0.
2. Ejecute al instalador en el equipo que tiene la instancia que desee separar.
2. El instalador identificará instancias locales que son candidatos para deshacer el enlace.
3. Anule la selección de la casilla de verificación situada junto a la instancia que desea revertir a la configuración original de SQL Server R Services.
4. Acepte el contrato de licencia para Microsoft R Server 9.1.0. Debe aceptar el contrato de licencia, incluso si se elimina el servidor de R.
5. Haga clic en **Finalizar**. El proceso tarda algún tiempo.

### <a name="unbind-using-the-command-line"></a>Deshacer el enlace mediante la línea de comandos

1. Abra un símbolo del sistema y vaya a la carpeta que contiene **sqlbindr.exe**, como se describe en la sección anterior.

2. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia.

   Por ejemplo, el comando siguiente restablece la instancia predeterminada:
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran los problemas conocidos específicos para usar de la utilidad SqlBindR.exe o a las actualizaciones mediante la utilidad de instalación de Microsoft R Server que afecta a las instancias de SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando los paquetes que estaban previamente instalados

En la utilidad de actualización que se incluye con Microsoft R Server 9.0.1, la utilidad no restauró los paquetes originales o componentes de R completo, que requieren que el usuario ejecute la reparación en la instancia, aplican todas las versiones de servicio y, a continuación, reinicie la instancia.

Sin embargo, la versión más reciente de la utilidad de actualización para Microsoft R Server 9.1.0, restaurará automáticamente las características de R originales. Por lo tanto, no es necesario volver a instalar los componentes de R o volver a aplicar la revisión del servidor. Sin embargo, todavía debe instalar los paquetes de R que pueden haber agregado tras la instalación inicial.

Si ha usado las funciones de administración de paquetes para instalar y compartir el paquete, esta tarea es mucho más fácil: puede usar comandos de R para sincronizar los paquetes instalados en el sistema de archivos con registros de la base de datos y viceversa. Para obtener más información, vea [instalar y administrar paquetes de R](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>No se puede realizar la actualización desde 9.0.1

Si previamente ha actualizado una instancia de SQL Server 2016 R Services a 9.0.1, al ejecutar el nuevo instalador de Microsoft R Server 9.1.0, mostrar una lista de todas las instancias válidas y, a continuación, de forma predeterminada, seleccione instancias enlazadas previamente. Si continúa, las instancias enlazadas previamente son independientes. Como resultado, el 9.0.1 anteriores se quita la instalación, los incluidos relacionados con los paquetes, pero no se instala la nueva versión de Microsoft R Server (9.1.0).

Como alternativa, puede modificar la instalación del servidor de R existente como se indica a continuación:
1. En el Panel de Control, abra **agregar o quitar programas**.
2. Busque Microsoft R Server y haga clic en **cambiar o modificar**.
3. Cuando se inicia el programa de instalación, seleccione las instancias que desea enlazar a 9.1.0.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Enlazar o desenlazar deja varias carpetas temporales

A veces, el enlace y operaciones Desenlazando producirá un error limpiar las carpetas temporales.
Si encuentra carpetas con un nombre parecido a esto, puede quitarlo una vez completada la instalación:`R_SERVICES_<guid>`

> [!NOTE]
> Asegúrese de esperar hasta que finalice la instalación. Puede tardar mucho tiempo para quitar las bibliotecas de R asociadas con una versión y, a continuación, agregar las nuevas bibliotecas de R. Cuando se complete la operación, se quitarán las carpetas temporales.

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

+ [Novedades de R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R Server problemas conocidos](https://docs.microsoft.com/r-server/resources-known-issues)

