---
title: Actualización de componentes de R y Python
description: Actualice R y Python en SQL Server Machine Learning Services o SQL Server R Services con sqlbindr. exe para enlazar con Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 948ce20bf32aaa2051c4a805a3ca2f131a7c0c8f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715212"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Actualización de los componentes de machine learning (R y Python) en instancias de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La integración de R y Python en SQL Server incluye paquetes de código abierto y de propiedad de Microsoft. En el servicio de SQL Server estándar, los paquetes se actualizan según el ciclo de versión SQL Server, con correcciones de errores en los paquetes existentes en la versión actual, pero sin actualizaciones de versiones principales. 

Sin embargo, muchos científicos de datos están acostumbrados a trabajar con paquetes más recientes a medida que estén disponibles. En el caso de SQL Server Machine Learning Services (en base de datos) y SQL Server R Services (en base de datos), puede obtener [las versiones más recientes de R y Python](#version-map) *enlazando* a **Microsoft machine learning Server**. 

## <a name="what-is-binding"></a>¿Qué es el enlace?

El enlace es un proceso de instalación que intercambia el contenido de las carpetas R_SERVICES y PYTHON_SERVICES con archivos ejecutables, bibliotecas y herramientas más recientes desde [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/index).

Junto con los componentes actualizados, se trata de un cambio en los modelos de servicio. En lugar de [SQL Server ciclo de vida del producto](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), con [SQL Server actualizaciones acumulativas](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), las actualizaciones del servicio ahora se ajustan a la [escala de tiempo de soporte técnico de Microsoft R Server & machine learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) en el [ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

A excepción de las versiones de los componentes y las actualizaciones del servicio, el enlace no cambia los aspectos básicos de la instalación: La integración de R y Python sigue siendo parte de una instancia del motor de base de datos, las licencias no se modifican (no hay costos adicionales asociados al enlace) y las directivas de soporte técnico de SQL Server siguen conservando para el motor de base de datos. En el resto de este artículo se explica el mecanismo de enlace y cómo funciona para cada versión de SQL Server.

> [!NOTE]
> El enlace se aplica a instancias de (en base de datos) que están enlazadas a instancias de SQL Server. El enlace no es relevante para una instalación (independiente).

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
**Consideraciones sobre el enlace de SQL Server 2017**

Por SQL Server Machine Learning Services, considere la posibilidad de enlazar solo cuando Microsoft Machine Learning Server comienza a ofrecer paquetes adicionales o versiones más recientes sobre lo que ya tiene.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Consideraciones sobre el enlace de SQL Server 2016**

En el caso de los clientes de SQL Server 2016 R Services, el enlace proporciona paquetes de R actualizados, paquetes nuevos que no forman parte de la instalación original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)) y [modelos](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)previamente entrenados, que se pueden actualizar en cada nueva versión principal y secundaria de [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/index). El enlace no proporciona compatibilidad con Python, que es una característica SQL Server 2017.
::: moniker-end

<a name="version-map"></a>

## <a name="version-map"></a>Asignación de versión

La tabla siguiente es un mapa de versión que muestra las versiones de paquete en los vehículos de versión para que pueda determinar posibles rutas de actualización al enlazar a Microsoft Machine Learning Server (conocido anteriormente como R Server, antes de que se haya agregado compatibilidad con Python. en MLS 9.2.1). 

Tenga en cuenta que el enlace no garantiza la versión más reciente de R o Anaconda. Al enlazar a Microsoft Machine Learning Server (MLS), obtiene la versión de R o Python que se instala a través del programa de instalación, que puede que no sea la versión más reciente disponible en la Web.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versión inicial | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9,1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9,3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) sobre R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | 3\.4.3 R |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9,1 |  9.2.1 |  9,3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[**SQL Server Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versión inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) sobre R | R 3.3.3 | 3\.4.3 R | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9,2 |  9,3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4,2 sobre Python 3,5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2  | 9,3| | | |
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2  | 9,3| | | |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9,2 | 9,3| | | |
::: moniker-end

## <a name="how-component-upgrade-works"></a>Cómo funciona la actualización de componentes 

Las bibliotecas y los ejecutables de r y Python se actualizan al enlazar una instalación existente de R y Python a Machine Learning Server. El [instalador de Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ejecuta el enlace al ejecutar el programa de instalación en una instancia existente del motor de base de datos de SQL Server que tiene integración de R o Python. El programa de instalación detecta las características existentes y le pide que vuelva a enlazar a Machine Learning Server. 

Durante el enlace, el contenido `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` de `\PYTHON_SERVICES` y se sobrescribe con los archivos ejecutables y las `C:\Program Files\Microsoft\ML Server\R_SERVER` bibliotecas `\PYTHON_SERVER`más recientes de y.

Al mismo tiempo, el modelo de mantenimiento también se voltea desde SQL Server mecanismos de actualización hasta el ciclo de versión principal y secundario más frecuente de Microsoft Machine Learning Server. Cambiar las directivas de soporte técnico es una opción atractiva para los equipos de ciencia de datos que requieren módulos de R y Python de nueva generación para sus soluciones. 

+ Sin enlace, los paquetes de R y Python se revisan para correcciones de errores al instalar una SQL Server Service Pack o una actualización acumulativa (CU). 
+ Con el enlace, se pueden aplicar versiones de paquetes más recientes a la instancia, independientemente de la programación de la versión de CU, en la [Directiva del ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy) y versiones de Microsoft machine learning Server. La Directiva de soporte técnico moderno del ciclo de vida ofrece actualizaciones más frecuentes en una duración de un año inferior. Después del enlace, seguiría usando el instalador de MLS para futuras actualizaciones de R y Python a medida que estén disponibles en los sitios de descarga de Microsoft.

El enlace solo se aplica a las características de R y Python. Es decir, los paquetes de código abierto para las características de R y Python (Microsoft R Open, Anaconda) y los paquetes de propiedad RevoScaleR, revoscalepy, etc. El enlace no cambia el modelo de compatibilidad de la instancia del motor de base de datos y no cambia la versión de SQL Server.

El enlace es reversible. Puede revertir a SQL Server el mantenimiento desenlazando [la instancia](#bkmk_Unbind) y reparing la instancia del motor de base de datos de SQL Server.

Resumen, los pasos para el enlace son los siguientes:

+ Comenzar con una instalación existente, configurada de SQL Server R Services o SQL Server Machine Learning Services.
+ Determine qué versión de Microsoft Machine Learning Server tiene los componentes actualizados que quiere usar.
+ Descargue y ejecute el programa de instalación de esa versión. El programa de instalación detecta la instancia existente, agrega una opción de enlace y devuelve una lista de instancias compatibles.
+ Elija la instancia que desea enlazar y, a continuación, finalice el programa de instalación para ejecutar el enlace.

En cuanto a la experiencia del usuario, la tecnología y la forma de trabajar con ella no cambian. La única diferencia es la presencia de paquetes de versiones más recientes y posiblemente paquetes adicionales no disponibles originalmente a través de SQL Server.

## <a name="bkmk_BindWizard"></a>Enlazar a MLS mediante el programa de instalación

El programa de instalación de Microsoft Machine Learning detecta las características existentes y SQL Server versión e invoca una utilidad llamada SqlBindR. exe para cambiar el enlace. Internamente, SqlBindR está encadenado al programa de instalación y se usa indirectamente. Más adelante, puede llamar a SqlBindR directamente desde la línea de comandos para ejecutar opciones específicas.

1. En SSMS, ejecute `SELECT @@version` para comprobar que el servidor cumple los requisitos mínimos de compilación. 

   En el caso de los servicios de SQL Server 2016 R, el mínimo es [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) y [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Compruebe la versión de los paquetes base de R y RevoScaleR para confirmar que las versiones existentes son inferiores a lo que tiene previsto reemplazar. 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. Cierre SSMS y cualquier otra herramienta que tenga una conexión abierta a SQL Server. El enlace sobrescribe los archivos de programa. Si SQL Server tiene sesiones abiertas, el enlace producirá un error con el código de error de enlace 6.

1. Descargue Microsoft Machine Learning Server en el equipo que tiene la instancia de que desea actualizar. Se recomienda la [versión más reciente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descomprima la carpeta e inicie programa. exe, que se encuentra en MLSWIN93.

   ![Asistente para la instalación de Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. En **configurar la instalación**, confirme los componentes que se van a actualizar y revise la lista de instancias compatibles. 

   Este paso es muy importante.

   A la izquierda, elija cada característica que desee conservar o actualizar. No puede actualizar algunas características y no otras. Una casilla vacía quita esa característica, suponiendo que está instalada actualmente. En la captura de pantalla, dada una instancia de SQL Server 2016 R Services (MSSQL13), R y la versión R de los modelos entrenados previamente se seleccionan. Esta configuración es válida porque SQL Server 2016 admite R pero no Python.

   Si va a actualizar componentes en SQL Server los servicios de 2016 R, no seleccione la característica de Python. No se puede Agregar Python a SQL Server 2016 R Services.

   A la derecha, active la casilla situada junto al nombre de la instancia. Si no hay ninguna instancia en la lista, tiene una combinación no compatible. Si no selecciona una instancia, se crea una nueva instalación independiente de Machine Learning Server y las bibliotecas de SQL Server no se modifican. Si no puede seleccionar una instancia, puede que no esté en [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Configurar paso de instalación](media/mls-931-installer-mssql13.png)

1. En la página **contrato de licencia** , seleccione Acepto **estos términos** para aceptar los términos de licencia de machine learning Server. 

1. En las páginas sucesivas, dé su consentimiento a condiciones de licencia adicionales para cualquier componente de código abierto que haya seleccionado, como Microsoft R Open o la distribución de Python Anaconda.

1. En la página **casi hay** , tome nota de la carpeta de instalación. La carpeta predeterminada es \Archivos de Programa\microsoft\ml Server.

    Si desea cambiar la carpeta de instalación, haga clic en **Opciones avanzadas** para volver a la primera página del asistente. Sin embargo, debe repetir todas las selecciones anteriores.

Durante el proceso de instalación, se reemplazan todas las bibliotecas de R o Python usadas por SQL Server y Launchpad se actualiza para usar los componentes más recientes. Como resultado, si la instancia usaba previamente bibliotecas en la carpeta R_SERVICES predeterminada, después de la actualización, estas bibliotecas se quitan y las propiedades del servicio Launchpad se cambian para usar las bibliotecas en la nueva ubicación.

El enlace afecta el contenido de estas carpetas: C:\Archivos de Programa\microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library se reemplaza por el contenido de C:\Archivos de Programa\microsoft\ml Server\R_SERVER. La segunda carpeta y su contenido se crean mediante el programa de instalación de Microsoft Machine Learning Server. 

Si se produce un error en la actualización, consulte los [códigos de error de SqlBindR](#sqlbindr-error-codes) para obtener más información.

## <a name="confirm-binding"></a>Confirmar enlace

Compruebe de nuevo la versión de R y RevoScaleR para confirmar que tiene versiones más recientes. Use la consola de R distribuida con los paquetes de R en la instancia del motor de base de datos para obtener información del paquete:

```sql
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

En el caso de los servicios SQL Server 2016 R enlazados a Machine Learning Server 9,3, el paquete base de R debe ser 3.4.3, RevoScaleR debe ser 9,3 y también debe tener MicrosoftML 9,3. 

Si agregó los modelos entrenados previamente, los modelos se incrustan en la biblioteca MicrosoftML y puede llamarlos a través de las funciones de MicrosoftML. Para obtener más información, vea [ejemplos de R para MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Enlace sin conexión (sin acceso a Internet)

En el caso de sistemas sin conectividad a Internet, puede descargar el instalador y los archivos. cab en un equipo conectado a Internet y, a continuación, transferir archivos al servidor aislado. 

El instalador (programa. exe) incluye los paquetes de Microsoft (RevoScaleR, MicrosoftML, olapr, sqlRUtils). Los archivos. cab proporcionan otros componentes principales. Por ejemplo, el archivo CAB "SRO" proporciona R Open, la distribución de R de código abierto de Microsoft.

Las instrucciones siguientes explican cómo colocar los archivos para una instalación sin conexión.

1. Descargue el instalador de MLS. Se descarga como un solo archivo comprimido. Se recomienda la [versión más reciente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), pero también puede instalar [las versiones anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Descargue los archivos. cab. Los vínculos siguientes son para la versión 9,3. Si necesita versiones anteriores, puede encontrar más vínculos en [R Server 9,1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Recuerde que Python/Anaconda solo se puede Agregar a una instancia de Machine Learning Services de SQL Server. Existen modelos previamente entrenados para R y Python; el archivo. cab proporciona modelos en los lenguajes que está utilizando.

    | Característica | Descargar |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos entrenados previamente | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transfiera los archivos. zip y. cab al servidor de destino.

1. En el servidor, escriba `%temp%` en el comando ejecutar para obtener la ubicación física del directorio Temp. La ruta de acceso física varía según la máquina, pero `C:\Users\<your-user-name>\AppData\Local\Temp`suele ser.

1. Coloque los archivos. cab en la carpeta% Temp%.

1. Descomprima el instalador.

1. Ejecute programa. exe y siga las indicaciones en pantalla para completar la instalación.

## <a name="bkmk_BindCmd"></a>Operaciones de línea de comandos

Después de ejecutar Microsoft Machine Learning Server, está disponible una utilidad de línea de comandos denominada SqlBindR. exe que se puede usar para operaciones de enlace adicionales. Por ejemplo, si decide invertir un enlace, puede volver a ejecutar el programa de instalación o usar la utilidad de línea de comandos. Además, puede usar esta herramienta para comprobar la compatibilidad y la disponibilidad de las instancias.

> [!TIP]
> ¿No encuentra SqlBindR? Probablemente no haya ejecutado el programa de instalación. SqlBindR solo está disponible después de ejecutar el programa de instalación de Machine Learning Server.

1. Abra un símbolo del sistema como administrador y vaya hasta la carpeta que contiene sqlbindr.exe. La ubicación predeterminada es C:\Archivos de Files\Microsoft\MLServer\Setup

2. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
  
   Anote el nombre completo de la instancia como se muestra. Por ejemplo, el nombre de la instancia podría ser MSSQL14. MSSQLSERVER para una instancia predeterminada o algo parecido a SERVERNAME. MYNAMEDINSTANCE.

3. Ejecute el comando **SqlBindR. exe** con el argumento */BIND* y especifique el nombre de la instancia que se va a actualizar con el nombre de instancia que se devolvió en el paso anterior.

   Por ejemplo, para actualizar la instancia predeterminada, escriba:`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Una vez completada la actualización, reinicie el servicio Launchpad asociado a cualquier instancia de que se haya modificado.

## <a name="bkmk_Unbind"></a>Revertir o desenlazar una instancia

Puede restaurar una instancia enlazada a una instalación inicial de los componentes de R y Python, establecida por SQL Server el programa de instalación. Hay tres partes para revertir al servicio de SQL Server.

+ [Paso 1: Desenlazar de Microsoft Machine Learning Server](#step-1-unbind)
+ [Paso 2: Restaurar la instancia a su estado original](#step-2-restore)
+ [Paso 3: Reinstalar los paquetes que ha agregado a la instalación](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Paso 1: Desenlazar

Tiene dos opciones para revertir el enlace: vuelva a ejecutar el programa de instalación o use la utilidad de línea de comandos SqlBindR.

#### <a name="bkmk_wizunbind"></a>Desenlazar con el programa de instalación

1. Busque el instalador de Machine Learning Server. Si ha quitado el instalador, es posible que tenga que descargarlo de nuevo o copiarlo desde otro equipo.
2. Asegúrese de ejecutar el instalador en el equipo que tiene la instancia de a la que desea desenlazar.
2. El instalador identifica las instancias locales que son candidatas para desenlazar.
3. Anule la selección de la casilla situada junto a la instancia que desea revertir a la configuración original.
4. Acepte el contrato de licencia. Debe indicar su aceptación de los términos de licencia incluso al instalar.
5. Haga clic en **Finalizar** El proceso tarda unos minutos.

#### <a name="bkmk_cmdunbind"></a>Desenlazar con la línea de comandos

1. Abra un símbolo del sistema y vaya a la carpeta que contiene **sqlbindr.exe**, como se describe en la sección anterior.

2. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia.

   Por ejemplo, el comando siguiente revierte la instancia predeterminada:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Paso 2: Reparación de la instancia de SQL Server

Ejecute el programa de instalación de SQL Server para reparar la instancia del motor de base de datos que tiene las características de R y Python. Se conservan las actualizaciones existentes, pero si se perdió alguna SQL Server las actualizaciones de servicio de los paquetes de R y Python, este paso aplica las revisiones.

Como alternativa, esto es más trabajo, pero también puede desinstalar completamente y reinstalar la instancia del motor de base de datos y, a continuación, aplicar todas las actualizaciones del servicio.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Paso 3: Agregar paquetes de terceros

Es posible que haya agregado otros paquetes de código abierto o de terceros a la biblioteca de paquetes. Como invertir el enlace cambia la ubicación de la biblioteca de paquetes predeterminada, debe volver a instalar los paquetes en la biblioteca que R y Python están usando ahora. Para obtener más información, vea [paquetes](../package-management/default-packages.md)predeterminados, [instalar nuevos paquetes de R](../r/install-additional-r-packages-on-sql-server.md)e [instalar nuevos paquetes de Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintaxis del comando SqlBindR. exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parámetros

|Name|Descripción|
|------|------|
|*list*| Muestra una lista de todos los identificadores de instancia de SQL Database en el equipo actual.|
|*bind*| Actualiza la instancia de SQL Database especificada a la versión más reciente de R Server y garantiza que la instancia obtenga automáticamente las actualizaciones futuras de R Server.|
|*unbind*|Desinstala la versión más reciente de R Server de la instancia de SQL Database especificada e impide que las actualizaciones futuras de R Server afecten a la instancia.|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Errores de enlace

El instalador de MLS y SqlBindR devuelven los siguientes mensajes y códigos de error.

|Código de error  | Message           | Detalles               |
|------------|-------------------|-----------------------|
|Error de enlace 0 | Correcto (correcto) | Enlace pasado sin errores. |
|Error de enlace 1 | Argumentos no válidos | Error de sintaxis. |
|Error de enlace 2 | Acción no válida | Error de sintaxis. |
|Error de enlace 3 | Instancia no válida | Existe una instancia de, pero no es válida para el enlace. |
|Error de enlace 4 | No enlazable | |
|Error de enlace 5 | Ya enlazado | Ha ejecutado el comando *bind* , pero la instancia especificada ya está enlazada. |
|Error de enlace 6 | Error de enlace | Se produjo un error al desenlazar la instancia. Este error puede producirse si se ejecuta el instalador de MLS sin seleccionar ninguna característica. El enlace requiere que seleccione una instancia de MSSQL y R y Python, suponiendo que la instancia es SQL Server 2017. Este error también se produce si SqlBindR no pudo escribir en la carpeta archivos de programa. Si abre sesiones o identificadores para SQL Server, se producirá este error. Si recibe este error, reinicie el equipo y rerepita los pasos de enlace antes de iniciar las sesiones nuevas.|
|Error de enlace 7 | Sin enlazar | La instancia del motor de base de datos tiene R Services o SQL Server Machine Learning Services. La instancia no está enlazada a Microsoft Machine Learning Server. |
|Error de enlace 8 | Error de desenlace | Se produjo un error al desenlazar la instancia. |
|Error de enlace 9 | No se encontraron instancias | No se encontraron instancias del motor de base de datos en este equipo. |

## <a name="known-issues"></a>Problemas conocidos

En esta sección se enumeran los problemas conocidos específicos del uso de la utilidad SqlBindR. exe o de las actualizaciones de Machine Learning Server que pueden afectar a las instancias de SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurar los paquetes que se instalaron previamente

Si actualizó a Microsoft R Server 9.0.1, la versión de SqlBindR. exe de esa versión no pudo restaurar los paquetes originales o los componentes de R por completo, lo que requiere que el usuario ejecute SQL Server reparación en la instancia, aplique todas las versiones de servicio y, a continuación, reinicie instancia de.

Una versión posterior de SqlBindR restaura automáticamente las características de R originales, lo que elimina la necesidad de reinstalar los componentes de R o volver a revisar el servidor. Sin embargo, debe instalar las actualizaciones de paquetes de R que se hayan agregado después de la instalación inicial.

Si ha usado los roles de administración de paquetes para instalar y compartir el paquete, esta tarea es mucho más sencilla: puede usar comandos de R para sincronizar paquetes instalados en el sistema de archivos mediante registros en la base de datos y viceversa. Para obtener más información, vea [Administración de paquetes de R para SQL Server](../r/install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas con varias actualizaciones desde SQL Server

Si ya ha actualizado una instancia de SQL Server 2016 R Services a 9.0.1, al ejecutar el nuevo instalador de Microsoft R Server 9.1.0, se muestra una lista de todas las instancias válidas y, a continuación, selecciona las instancias enlazadas previamente de forma predeterminada. Si continúa, las instancias enlazadas anteriormente no estarán enlazadas. Como resultado, se quita la instalación anterior de 9.0.1, incluidos los paquetes relacionados, pero no se instala la nueva versión de Microsoft R Server (9.1.0).

Como solución alternativa, puede modificar la instalación de R Server existente como se indica a continuación:
1. En el panel de control, Abra **Agregar o quitar programas**.
2. Busque Microsoft R Server y haga clic en **cambiar/modificar**.
3. Cuando se inicie el programa de instalación, seleccione las instancias que desea enlazar a 9.1.0.

Microsoft Machine Learning Server 9.2.1 y 9,3 no tienen este problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Enlazar o Desenlazar deja varias carpetas temporales

A veces, las operaciones de enlace y desenlace no pueden limpiar las carpetas temporales.
Si encuentra carpetas con un nombre como este, puede quitarlo una vez completada la instalación: R_SERVICES_<guid>

> [!NOTE]
> Asegúrese de esperar hasta que se complete la instalación. Puede tardar mucho tiempo en quitar las bibliotecas de R asociadas a una versión y, a continuación, agregar las nuevas bibliotecas de R. Una vez finalizada la operación, se quitan las carpetas temporales.

## <a name="see-also"></a>Vea también

+ [Instalación de Machine Learning Server para Windows (conexión a Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar Machine Learning Server para Windows (sin conexión)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conocidos de Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anuncios de características de la versión anterior de R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Características desusadas, descontinuadas o modificadas](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
