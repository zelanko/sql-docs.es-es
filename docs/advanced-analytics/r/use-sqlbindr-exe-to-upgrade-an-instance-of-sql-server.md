---
title: Actualizar los componentes de R y Python en instancias de SQL Server R (servicios de aprendizaje de máquina) | Documentos de Microsoft
description: Actualizar R y Python en SQL Server 2016 R Services o SQL Server de 2017 Machine Learning Services mediante sqlbindr.exe para enlazar con el servidor de aprendizaje de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 140d84717f7343f52b1c553964cce8f0c40e2c7c
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Actualizar los componentes de aprendizaje (R y Python) de máquina en instancias de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La integración de R y Python en SQL Server incluye paquetes de código abierto y propietario de Microsoft. En el servicio de SQL Server estándar, los paquetes de R y Python se actualizan según el ciclo de versiones de SQL Server, con correcciones de errores para los paquetes existentes en la versión actual. 

La mayoría de los científicos de datos están acostumbrados a trabajar con paquetes más reciente cuando estén disponibles. Para SQL Server de 2017 Machine Learning Services (In-Database) y SQL Server 2016 R Services (In-Database), puede obtener versiones más recientes de R y Python cambiando el *enlace* de mantenimiento de SQL Server para [Microsoft Servidor de aprendizaje de máquina](https://docs.microsoft.com/en-us/machine-learning-server/index) y [directiva de soporte técnico de ciclo de vida moderna](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Enlace no cambia los fundamentos de la instalación: integración de R y Python sigue formando parte de una instancia del motor de base de datos, Administrador de licencias no se ha cambiado (sin costo adicional asociado enlace) y siguen ofreciendo las directivas de soporte técnico de SQL Server para la base de datos motor de búsqueda. Pero reenlace cambiar cómo se procesan los paquetes de R y Python. El resto de este artículo explica el mecanismo de enlace y cómo funciona para cada versión de SQL Server.

> [!NOTE]
> Enlace se aplica a solo instancias (en bases de datos). Enlace no es relevante para una instalación (independiente).

**SQL Server 2017**

Para servicios de aprendizaje de máquina de 2017 de SQL Server, puede considerar enlace solo cuando comienza a servidor de aprendizaje de máquina de Microsoft ofrecer paquetes adicionales o versiones más recientes sobre lo que ya tienen.

**SQL Server 2016**

Para los clientes de SQL Server 2016 R Services, hay dos rutas de acceso para obtener nuevos y actualizados paquetes de R. Uno conlleva la actualización a SQL Server 2017; el segundo, enlace al servidor de aprendizaje de máquina de Microsoft.

Actualizar a SQL Server 2017 obtiene paquetes de R en las versiones incluidas en esa versión, además de las características de Python. O bien, obtiene de enlace se actualizan paquetes de R, que pueden actualizarse más en cada nueva versión principal y secundaria del servidor de aprendizaje de máquina de Microsoft. Enlace no ofrece soporte de Python, que es una característica de SQL Server 2017. 

**Actualizaciones de componentes disponibles a través del servidor de aprendizaje de máquina de Microsoft**

En la tabla siguiente es un mapa de versión, que muestra la versión instalada con SQL Server, con las posibles actualizaciones cuando se enlace al servidor de aprendizaje de máquina de Microsoft (anteriormente conocido como R Server antes de la adición de compatibilidad con Python a partir de MLS 9.2.1). 

Tenga en cuenta que el enlace no garantiza la última versión de R o Anaconda. Cuando se enlaza al servidor de aprendizaje de máquina de Microsoft, obtenga la versión de R o Python instalada mediante el programa de instalación, que puede ser o no la versión más reciente disponible en la web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versión inicial | R Server 9.0.1 | R Server 9.1 | MLS 9.2.1 | MLS 9.3 |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) a través de R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/achine-learning-server/r-reference/revoscaler/revoscaler) | 9.0 | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1,0 |  1,0 |  1,0 |  1,0 |
[OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1,0 |  1,0 |  1,0 |  1,0 |


[**Servicios de aprendizaje de máquina de 2017 de SQL Server**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versión inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) a través de R | R 3.4.1 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.3 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.3  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1,0 |  1,0 | | | |
[OlapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1,0 |  1,0 | | | |
Anaconda 4.2 sobre Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.3  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.3  | 9.3| | | |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.3 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>Cómo funciona la actualización del componente

Actualización del componente es a través de *enlace* una instancia de SQL Server 2016 R Services (o una instancia de SQL Server de 2017 Machine Learning Services) al servidor de aprendizaje de máquina de Microsoft. [Aprendizaje de máquina de Microsoft Server](https://docs.microsoft.com/machine-learning-server/index) es un producto de servidor local independientes de SQL Server, pero con el mismo intérpretes y paquetes. Enlace intercambios fuera el mecanismo de actualización de servicio de SQL Server para que pueda utilizar los paquetes R y Python de envío con el servidor de aprendizaje de máquina de Microsoft, que a menudo son más recientes que las proporcionadas por el servicio de SQL Server. Las directivas de compatibilidad con conmutación es una opción atractiva para los equipos de la ciencia de datos que requieren más reciente generación R y módulos de Python para sus soluciones. 

Enlace es ejecutado por el [instalador MLS](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install). El programa de instalación actualiza paquetes de R y Python específicos, pero no sustituye a la instancia de base de datos de SQL Server con una independiente, la instalación de servidor desconectada.

+ Sin enlace, los paquetes de R y Python se han modificado para correcciones de errores al instalar un service pack de SQL Server o la actualización acumulativa (CU). 
+ Con el enlace, las versiones más recientes de paquete pueden aplicarse a la instancia, independientemente de la programación de la versión CU, en la [directiva de ciclo de vida moderna](https://support.microsoft.com/help/30881/modern-lifecycle-policy) y las versiones del servidor de aprendizaje de máquina de Microsoft. La directiva de soporte técnico de ciclo de vida moderna ofrece actualizaciones más frecuentes sobre una duración más corta, durante un año. 

Enlace se aplica a funciones de R y Python. Es decir, los paquetes de código abierto para características de R y Python (Microsoft R Open, Anaconda) y el propietario paquetes RevoScaleR, revoscalepy y así sucesivamente. Enlace no cambia el modelo de compatibilidad para la instancia del motor de base de datos y no cambia la versión de SQL Server.

El enlace es reversible. Puede revertir al mantenimiento de SQL Server por [desenlazar la instancia](#bkmk_Unbind) y reparing la instancia del motor de base de datos de SQL Server.

Sumarse al mismo tiempo, son los siguientes pasos para el enlace:

+ Empezar con una instalación existente, configurada de SQL Server 2016 R Services (o servicios de aprendizaje de SQL Server de 2017 máquina).
+ Determinar qué versión del servidor de aprendizaje de máquina de Microsoft tiene los componentes actualizados que desea usar.
+ Descargue y ejecute el programa de instalación de esa versión. El programa de instalación detecta la instancia existente, agrega una opción de enlace y devuelve una lista de instancias compatibles.
+ Elija la instancia que desea enlazar y, a continuación, finalice el programa de instalación para ejecutar el enlace.

En cuanto a la experiencia del usuario, la tecnología y cómo trabajar con la se ha modificado. La única diferencia es la presencia de los paquetes más recientes con control de versiones y posiblemente, otros paquetes originalmente no están disponibles a través de SQL Server (por ejemplo, MicrosoftML para los clientes de SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Actualizar mediante el programa de instalación

Configuración de aprendizaje del equipo de Microsoft detecta las características existentes y la versión de SQL Server y se invoca una utilidad denominada SqlBindR.exe para cambiar el enlace. Internamente, SqlBindR está enlazado con el programa de instalación y utilizar indirectamente. Más adelante, puede ejecutar SqlBindR directamente desde la línea de comandos para ejecutar opciones específicas.

1. Comprobar la versión de R y RevoScaleR para confirmar que son inferiores a los que planea sustituirlas por las versiones existentes. Para obtener más información, consulte [obtener R y Python empaquetar la información de](determine-which-packages-are-installed-on-sql-server.md).

1. [Descargar Microsoft máquina aprendizaje Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer) en el equipo que tiene la instancia que desea actualizar. 

1. Descomprima la carpeta e iniciar el programa de instalación.

    ![Asistente para la instalación de servidor de aprendizaje de máquina de Microsoft](media/mls-921-installer-start.PNG)

1. En **configurar la instalación**, confirme los componentes que desea actualizar y revisar la lista de instancias compatibles. 

   En la izquierda, seleccione todas las características que desea mantener o actualizar. No puede actualizar algunas de las características y otras no. Una casilla vacía indica que desea que esta característica quita suponiendo que actualmente está instalado. En la captura de pantalla, se selecciona una instancia de SQL Server de 2017 Machine Learning Services (MSSQL14) con R y Python. Esta configuración se admite porque SQL Server 2017 tiene R y Python.

   A la derecha, active la casilla situada junto al nombre de instancia. Si no aparece ninguna instancia, tendrá una combinación incompatible. Si no selecciona una instancia, se crea una nueva instalación independiente del servidor de aprendizaje de máquina y las bibliotecas de SQL Server son iguales.

    ![Asistente para la instalación de servidor de aprendizaje de máquina de Microsoft](media/configure-the-installation.PNG)

1. En el **del acuerdo de licencia** página, seleccione **acepto estos términos** para aceptar los términos de licencia para el servidor de aprendizaje de máquina. 

1. En las páginas sucesivas, dar su consentimiento a las condiciones de licencias adicionales para los componentes de código abierto que ha seleccionado, como Microsoft R Open o la distribución de Anaconda de Python.

1. En el **casi** página, tome nota de la carpeta de instalación. La carpeta predeterminada es \Program Files\Microsoft\ML Server.

    Si desea cambiar la carpeta de instalación, haga clic en **avanzadas** para volver a la primera página del asistente. Sin embargo, debe repetir todas las selecciones anteriores.

1. Si está [instalar componentes sin conexión](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline), le podrían solicitar para la ubicación de los componentes de aprendizaje necesaria del equipo, como Microsoft R Open, servidor de Python y Python abierta.

Durante el proceso de instalación, se reemplazan las bibliotecas de R o Python utilizadas por SQL Server y Launchpad se actualiza para usar los componentes más recientes. Como resultado, si la instancia había utilizado previamente bibliotecas en la carpeta R_SERVICES de manera predeterminada, después de la actualización se quitan estas bibliotecas y se cambian las propiedades para el servicio Launchpad, para usar las bibliotecas en la nueva ubicación.

Enlace afecta al contenido de estas carpetas: C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library se reemplaza con el contenido de C:\Program Files\Microsoft\ML Server\R_SERVER. La segunda carpeta y su contenido se crea mediante el programa de instalación de servidor de Microsoft máquina aprendizaje. 

## <a name="confirm-binding"></a>Confirme el enlace

Volver a comprobar la versión de R y RevoScaleR para confirmar que tiene las versiones más recientes. Para obtener más información, consulte [obtener R y Python empaquetar la información de](determine-which-packages-are-installed-on-sql-server.md). Los clientes de SQL Server 2016 R Services también deben tener MicrosoftML.

## <a name="bkmk_BindCmd"></a>Operaciones de línea de comandos

Después de ejecutar el servidor de aprendizaje de máquina de Microsoft, una utilidad de línea de comandos denominada SqlBindR.exe deja de estar disponible que se pueden utilizar para aún más las operaciones de enlace. Por ejemplo, si decide invertir un enlace, se puede volver a ejecutar el programa de instalación o use la utilidad de línea de comandos. Además, puede usar esta herramienta para comprobar por ejemplo, compatibilidad y la disponibilidad.

> [!TIP]
> ¿No se puede encontrar SqlBindR? Probablemente no ha ejecutado el programa de instalación. SqlBindR está disponible sólo después de ejecutar el programa de instalación del servidor de aprendizaje de máquina.

1. Abra un símbolo del sistema como administrador y vaya hasta la carpeta que contiene sqlbindr.exe. La ubicación predeterminada es C:\Program Files\Microsoft\MLServer\Setup

2. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
  
   Anote el nombre completo de la instancia como se muestra. Por ejemplo, el nombre de instancia podría ser MSSQL14. MSSQLSERVER para una instancia predeterminada, o algo parecido a SERVERNAME. MYNAMEDINSTANCE.

3. Ejecute el **SqlBindR.exe** comando con el */enlazar* argumento y especifique el nombre de la instancia a actualizar, utilizando el nombre de instancia que se devuelve en el paso anterior.

   Por ejemplo, para actualizar la instancia predeterminada, escriba:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Una vez finalizada la actualización, reinicie el servicio de Launchpad asociado a cualquier instancia que se ha modificado.

## <a name="bkmk_Unbind"></a>Revertir o desenlazar una instancia

Puede restaurar una instancia enlazada a una instalación inicial de los componentes de R y Python, establecida por el programa de instalación de SQL Server. Hay tres partes para volver a los servicios de SQL Server.

+ [Paso 1: Deshacer el enlace con el servidor de aprendizaje de automático de Microsoft](#step-1-unbind)
+ [Paso 2: Restaurar la instancia al estado original](#step-2-restore)
+ [Paso 3: Vuelva a instalar todos los paquetes que agregan a la instalación](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Paso 1: desenlazar

Tiene dos opciones para revertir el enlace: vuelva a ejecutar el programa de instalación o use la utilidad de línea de comandos de SqlBindR.

#### <a name="bkmk_wizunbind"></a> Deshacer el enlace con el programa de instalación

1. Busque el programa de instalación de servidor de aprendizaje de máquina. Si ha quitado el programa de instalación, tendrá que descargarlo de nuevo, o copiarlo desde otro equipo.
2. Asegúrese de ejecutar el programa de instalación en el equipo que tiene la instancia que desee separar.
2. El programa de instalación identifica las instancias locales que son candidatos para deshacer el enlace.
3. Anule la selección de la casilla de verificación situada junto a la instancia que se va a volver a la configuración original.
4. Acepte el contrato de licencia. Debe indicar su aceptación de términos de licencia incluso cuando se instala.
5. Haga clic en **Finalizar**. El proceso tarda algún tiempo.

#### <a name="bkmk_cmdunbind"></a> Deshacer el enlace mediante la línea de comandos

1. Abra un símbolo del sistema y vaya a la carpeta que contiene **sqlbindr.exe**, como se describe en la sección anterior.

2. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia.

   Por ejemplo, el comando siguiente restablece la instancia predeterminada:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Paso 2: Repare la instancia de SQL Server

Ejecute el programa de instalación de SQL Server para reparar la instancia del motor de base de datos con las características de R y Python. Las actualizaciones existentes se conservan, pero si se perdió las actualizaciones a los paquetes de R y Python de servicios de SQL Server, este paso aplica a las revisiones.

Como alternativa, se trata más trabajo, pero podría también totalmente desinstalar y volver a instalar la instancia del motor de base de datos y, a continuación, aplique todas las actualizaciones de servicio.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Paso 3: Agregar los paquetes de terceros

Puede que haya agregado otros paquetes de terceros o de código abierto a la biblioteca del paquete. Puesto que invertir el enlace, cambia la ubicación de la biblioteca de paquetes de forma predeterminada, debe volver a instalar los paquetes a la biblioteca que está usando ahora R y Python. Para obtener más información, consulte [predeterminado paquetes](installing-and-managing-r-packages.md), [instalar nuevos paquetes de R](install-additional-r-packages-on-sql-server.md), y [instalar nuevos paquetes de Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran problemas conocidos específicos para usar de la utilidad SqlBindR.exe o a las actualizaciones del servidor de aprendizaje de máquina que podrían afectar a instancias de SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurando los paquetes que estaban previamente instalados

Si ha actualizado a Microsoft R Server 9.0.1, la versión de SqlBindR.exe para esa versión no se pudo restaurar los paquetes originales o componentes de R por completo, que requieren que el usuario ejecute la reparación de SQL Server en la instancia, aplican todas las versiones de servicio y, a continuación, reiniciar la instancia.

Una versión posterior de SqlBindR automáticamente restaurar las características de R originales, lo que elimina la necesidad de volver a instalar componentes de R o volver a aplicar la revisión del servidor. Sin embargo, debe instalar las actualizaciones de paquete de R que pueden haber agregado tras la instalación inicial.

Si ha usado las funciones de administración de paquetes para instalar y compartir el paquete, esta tarea es mucho más fácil: puede usar comandos de R para sincronizar los paquetes instalados en el sistema de archivos con registros de la base de datos y viceversa. Para obtener más información, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas con varias actualizaciones de SQL Server

Si previamente ha actualizado una instancia de SQL Server 2016 R Services a 9.0.1, al ejecutar el nuevo instalador de Microsoft R Server 9.1.0, muestra una lista de todas las instancias válidas y, a continuación, de forma predeterminada, selecciona instancias enlazadas previamente. Si continúa, las instancias enlazadas previamente son independientes. Como resultado, el 9.0.1 anteriores se quita la instalación, los incluidos relacionados con los paquetes, pero no se instala la nueva versión de Microsoft R Server (9.1.0).

Como alternativa, puede modificar la instalación del servidor de R existente como se indica a continuación:
1. En el Panel de Control, abra **agregar o quitar programas**.
2. Busque Microsoft R Server y haga clic en **cambiar o modificar**.
3. Cuando se inicia el programa de instalación, seleccione las instancias que desea enlazar a 9.1.0.

Aprendizaje de máquina Microsoft Server 9.2.1 y 9.3 no tiene este problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Enlazar o desenlazar deja varias carpetas temporales

A veces, el enlace y operaciones Desenlazando producirá un error limpiar las carpetas temporales.
Si encuentra carpetas con un nombre parecido a esto, puede quitar una vez completada la instalación: R_SERVICES_<guid>

> [!NOTE]
> Asegúrese de esperar hasta que finalice la instalación. Puede tardar mucho tiempo para quitar las bibliotecas de R asociadas con una versión y, a continuación, agregar las nuevas bibliotecas de R. Cuando se complete la operación, se quitan las carpetas temporales.

## <a name="sqlbindrexe-command-syntax"></a>Sintaxis del comando SqlBindR.exe

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

## <a name="see-also"></a>Vea también

+ [Instalar equipo aprendizaje Server para Windows (conectado a Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar equipo aprendizaje para Windows del servidor (sin conexión)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conocidos en el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anuncios de características de la versión anterior del servidor de R](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Características desusadas, discontinuos o modificadas](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)