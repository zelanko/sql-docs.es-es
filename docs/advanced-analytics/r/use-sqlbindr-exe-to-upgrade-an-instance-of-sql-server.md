---
title: Actualizar los componentes de R y Python en instancias de SQL Server (servicios de Machine Learning) | Microsoft Docs
description: Actualización de R y Python en SQL Server 2016 Services o SQL Server 2017 Machine Learning Services usar sqlbindr.exe para enlazar a Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c2677885719c0b9a54a39b1609a0c2652728820f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078895"
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>Actualizar componentes de machine learning (R y Python) en instancias de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integración de R y Python en SQL Server incluye paquetes de código abierto y la propiedad de Microsoft. En el servicio de SQL Server estándar, los paquetes se actualizan según el ciclo de lanzamiento de SQL Server con correcciones de errores para los paquetes existentes desde la versión actual, pero no hay actualizaciones de versión principal. 

Sin embargo, muchos científicos de datos están acostumbrados a trabajar con los paquetes más recientes cuando estén disponibles. Para SQL Server 2017 Machine Learning Services (In-Database) y SQL Server 2016 R Services (In-Database), puede obtener [versiones más recientes de R y Python](#version-map) por *enlace* a **Microsoft Machine Learning Server**. 

## <a name="what-is-binding"></a>¿Qué es el enlace?

El enlace es un proceso de instalación que intercambia el contenido de las carpetas R_SERVICES y PYTHON_SERVICES con versiones más recientes ejecutables, bibliotecas y las herramientas de [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Junto con los componentes actualizados incluye un modificador en modelos de servicio. En lugar de la [ciclo de vida del producto de SQL Server](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017), con [actualizaciones acumulativas de SQL Server](https://support.microsoft.com/help/4047329/sql-server-2017-build-versions), las actualizaciones de servicio ahora se ajustan a la [admite la escala de tiempo para Microsoft R Server & máquina Servidor de aprendizaje](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) en el [ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Excepto en las versiones de componente y las actualizaciones del servicio, enlace no cambia los aspectos básicos de la instalación: integración de R y Python sigue siendo parte de una instancia del motor de base de datos, las licencias no ha cambiado (sin costos adicionales asociados con el enlace) y SQL Siguen ofreciendo las directivas de soporte técnico de servidor para el motor de base de datos. El resto de este artículo explica el mecanismo de enlace y su funcionamiento para cada versión de SQL Server.

> [!NOTE]
> Enlace se aplica a las instancias (en bases de datos) solo que están enlazadas a instancias de SQL Server. Enlace no es relevante para una instalación (independiente).

**Consideraciones de enlace de SQL Server 2017**

Para SQL Server 2017 Machine Learning Services consideraría enlace solo cuando Microsoft Machine Learning Server comienza a ofrecer más paquetes o las versiones más recientes sobre lo que ya tienen.

**Consideraciones de enlace de SQL Server 2016**

Para los clientes de SQL Server 2016 R Services, el enlace proporciona paquetes de R actualizados, nuevos paquetes no forma parte de la instalación original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)), y [modelos previamente aprendidos](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models), todos los cuales pueden ser aún más actualizar en cada nueva versión principal y secundaria de [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index). Enlace no le proporciona compatibilidad con Python, que es una característica de SQL Server 2017. 

<a name="version-map"></a>

## <a name="version-map"></a>Asignación de versión

En la tabla siguiente es un mapa de versión, que muestra las versiones del paquete a través de los vehículos de lanzamiento, por lo que puede determinar posibles rutas de actualización al enlazar a Microsoft Machine Learning Server (anteriormente conocido como R Server, antes de la adición de compatibilidad de Python a partir en MLS 9.2.1). 

Tenga en cuenta que el enlace no garantiza la versión más reciente de R o Anaconda. Al enlazar a Microsoft Machine Learning Server (MLS), obtenga la versión de R o Python instalada mediante instalación, que puede no ser la última versión disponible en la web.

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versión inicial | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [MLS 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [MLS 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
Microsoft R Open (MRO) a través de R | R 3.2.2     | R 3.3.2   |3.3.3 R   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1,0 |  1,0 |  1,0 |  1,0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1,0 |  1,0 |  1,0 |  1,0 |


[**SQL Server 2017 Machine Learning Services**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versión inicial | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
Microsoft R Open (MRO) a través de R | 3.3.3 R | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1,0 |  1,0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1,0 |  1,0 | | | |
Anaconda 4.2 sobre Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[modelos previamente entrenados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>Cómo funciona la actualización del componente 

Al enlazar una instalación existente de R y Python en Machine Learning Server, se actualizan los archivos ejecutables y bibliotecas de R y Python. Enlace que se ejecuta en el [instalador de Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) al ejecutar el programa de instalación en una existente database engine instancia de SQL Server 2016 o 2017, con la integración de R o Python. El programa de instalación detecta las características existentes y le pedirá que vuelva a enlazar a Machine Learning Server. 

Durante el enlace, el contenido de C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES y \PYTHON_SERVICES se sobrescriben con los archivos ejecutables y bibliotecas de C:\Program programa\microsoft\ml Server\R_SERVER y \PYTHON_SERVER más reciente.

Al mismo tiempo, el modelo de mantenimiento también se voltea los mecanismos de actualización de SQL Server, para el ciclo de versiones principales y secundarias más frecuente de Microsoft Machine Learning Server. Cambiar las directivas de soporte técnico es una opción atractiva para equipos de ciencia de datos que requieren una nueva generación de R y los módulos de Python para sus soluciones. 

+ Sin enlace, paquetes R y Python se han revisado para correcciones de errores al instalar un service pack de SQL Server o la actualización acumulativa (CU). 
+ Con el enlace, las versiones más recientes de paquete se pueden aplicar a la instancia, independientemente de la programación de lanzamiento CU, bajo el [directiva de ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy) y versiones de Microsoft Machine Learning Server. La directiva de soporte técnico del ciclo de vida moderno ofrece actualizaciones más frecuentes sobre una duración más corta de un año. Posterior al enlace, seguiría usar al instalador MLS para actualizaciones futuras de R y Python cuando estén disponibles en los sitios de descarga de Microsoft.

Enlace se aplica a funciones de R y Python. Es decir, los paquetes de código abierto para las características de R y Python (Anaconda, Microsoft R Open) y el propietario de paquetes de RevoScaleR, revoscalepy y así sucesivamente. Enlace no cambia el modelo de compatibilidad para la instancia del motor de base de datos y no cambia la versión de SQL Server.

El enlace es reversible. Puede revertir al servicio de SQL Server mediante una [desenlazar la instancia](#bkmk_Unbind) y reparing la instancia del motor de base de datos de SQL Server.

Sumó, son los siguientes pasos para el enlace:

+ Comience con una instalación existente configurada de SQL Server 2016 R Services (o Machine Learning Services de SQL Server 2017).
+ Determinar qué versión de Microsoft Machine Learning Server tiene los componentes actualizados que desee utilizar.
+ Descargue y ejecute el programa de instalación de esa versión. El programa de instalación detecta la instancia existente, agrega una opción de enlace y devuelve una lista de instancias compatibles.
+ Elija la instancia que desea enlazar y, a continuación, finalice el programa de instalación para ejecutar el enlace.

En cuanto a la experiencia del usuario, se modifica la tecnología y cómo trabajar con él. La única diferencia es la presencia de paquetes con versiones más recientes y, posiblemente, otros originalmente no están disponibles a través de SQL Server (por ejemplo, MicrosoftML para los clientes de SQL Server 2016 R Services).

## <a name="bkmk_BindWizard"></a>Enlazar a MLS mediante el programa de instalación

Instalación de Microsoft Machine Learning detecta las características existentes y la versión de SQL Server y se invoca una utilidad denominada SqlBindR.exe para cambiar el enlace. Internamente, SqlBindR está enlazado con el programa de instalación y utilizar indirectamente. Más adelante, puede llamar a SqlBindR directamente desde la línea de comandos que actúan sobre opciones específicas.

1. En SSMS, ejecute `SELECT @@version` para comprobar que el servidor cumple los requisitos mínimos de compilación. 

   Para SQL Server 2016 R Services, el valor mínimo es [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) y [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Compruebe la versión de base de R y paquetes de RevoScaleR para confirmar las versiones existentes son menores que planea reemplácelas con. Para SQL Server 2016 R Services, paquete de R Base es 3.2.2 y RevoScaleR es 8.0.3.

    ```SQL
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

1. Cierre SSMS y otras herramientas de tener una conexión abierta a SQL Server. Enlace sobrescribe los archivos de programa. Si SQL Server tiene sesiones abiertas, se producirá un error de enlace con el código de error de enlace 6.

1. Descargue Microsoft Machine Learning Server en el equipo que tiene la instancia que desea actualizar. Se recomienda la [versión más reciente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descomprima la carpeta e iniciar ServerSetup.exe, ubicado en MLSWIN93.

   ![Asistente para la instalación de Microsoft Machine Learning Server](media/mls-921-installer-start.PNG)

1. En **configurar la instalación**, confirme los componentes para actualizar y revisar la lista de instancias compatibles. 

   Este paso es muy importante.

   En el lado izquierdo, elija todas las características que desea mantener o actualizar. No puede actualizar algunas de las características y otras no. Una casilla vacía, quita esa característica, suponiendo que actualmente está instalado. En la captura de pantalla, dada una instancia de SQL Server 2016 R Services (MSSQL13), se seleccionan R y la versión de R de los modelos previamente entrenados. Esta configuración es válida porque SQL Server 2016 admite R, pero no de Python.

   Si va a actualizar los componentes en SQL Server 2016 R Services, no seleccione la característica de Python. No se puede agregar Python a SQL Server 2016 R Services.

   A la derecha, active la casilla situada junto al nombre de instancia. Si no aparece ninguna instancia, tener una combinación incompatible. Si no selecciona una instancia, se crea una nueva instalación independiente de Machine Learning Server y las bibliotecas de SQL Server son iguales. Si no puede seleccionar una instancia, pueden no estar en [SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1). 

    ![Asistente para la instalación de Microsoft Machine Learning Server](media/mls-931-installer-mssql13.png)

1. En el **contrato de licencia** página, seleccione **acepto estos términos** para aceptar los términos de licencia para Machine Learning Server. 

1. En las páginas sucesivas, dar su consentimiento a condiciones de licencias adicionales para los componentes de código abierto seleccionado, como Microsoft R Open o la distribución de Anaconda Python.

1. En el **casi** página, tome nota de la carpeta de instalación. La carpeta predeterminada es \Program Files\Microsoft\ML Server.

    Si desea cambiar la carpeta de instalación, haga clic en **avanzadas** para volver a la primera página del asistente. Sin embargo, debe repetir todas las selecciones anteriores.

Durante el proceso de instalación, se reemplazan las bibliotecas de R o Python usadas SQL Server y Launchpad se actualiza para usar los componentes más recientes. Como resultado, si la instancia había utilizado previamente las bibliotecas en la carpeta R_SERVICES de forma predeterminada, después de actualizar estas bibliotecas se quitan y se cambian las propiedades para el servicio Launchpad para usar las bibliotecas en la nueva ubicación.

Enlace afecta al contenido de estas carpetas: C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library se reemplaza con el contenido de C:\Program programa\microsoft\ml Server\R_SERVER. La segunda carpeta y su contenido se crea mediante el programa de instalación de Microsoft Machine Learning Server. 

Si se produce un error en la actualización, compruebe [códigos de error SqlBindR](#sqlbindr-error-codes) para obtener más información.

## <a name="confirm-binding"></a>Confirme el enlace

Vuelva a comprobar la versión de R y RevoScaleR para confirmar que tiene las versiones más recientes. Use la consola de R distribuida con los paquetes de R en la instancia del motor de base de datos para obtener información de paquete:

```SQL
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

Para SQL Server 2016 R Services enlazado a Machine Learning Server 9.3, paquete de R Base debe ser 3.4.3, RevoScaleR debe ser 9.3 y también debe tener MicrosoftML 9.3. 

Si ha agregado los modelos previamente entrenados, los modelos se incrustan en la biblioteca de MicrosoftML y que se les puede llamar a través de funciones de MicrosoftML. Para obtener más información, consulte [ejemplos de R para MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml).

## <a name="offline-binding-no-internet-access"></a>Enlace sin conexión (sin acceso a internet)

Para sistemas sin conectividad a internet, puede descargar los archivos .cab y el instalador en una máquina conectada a internet y, a continuación, transferir archivos al servidor aislado. 

El instalador (ServerSetup.exe) incluye los paquetes de Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). Los archivos .cab proporcionan otros componentes principales. Por ejemplo, el archivo cab "SRO" proporciona R Open, la distribución de Microsoft de r de código abierto.

Las instrucciones siguientes explican cómo colocar los archivos de una instalación sin conexión.

1. Descargue al instalador de SAM. Descarga como un único archivo comprimido. Se recomienda la [versión más reciente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), pero también puede instalar [versiones anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Descargar archivos .cab. Los vínculos siguientes son para la versión 9.3. Si necesita las versiones anteriores, encontrará vínculos adicionales en [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Recuerde que Python/Anaconda solo pueden agregarse a una instancia de SQL Server 2017 Machine Learning Services. Existen modelos previamente entrenados para R y Python; el archivo .cab proporciona modelos en los idiomas que está usando.

    | Característica | Descargar |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos entrenados previamente | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transferir archivos .zip o .cab en el servidor de destino.

1. En el servidor, escriba `%temp%` en el comando de ejecución para obtener la ubicación física del directorio temporal. La ruta de acceso física varía según el equipo, pero suele ser `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Coloque los archivos .cab en la carpeta % temp %.

1. Descomprima el programa de instalación.

1. Ejecute ServerSetup.exe y siga las indicaciones en pantalla para completar la instalación.

## <a name="bkmk_BindCmd"></a>Operaciones de línea de comandos

Después de ejecutar Microsoft Machine Learning Server, una utilidad de línea de comandos denominada SqlBindR.exe disponible que puede usar para las operaciones de enlace aún más. Por ejemplo, si decide invertir un enlace, se podría volver a ejecutar el programa de instalación o usar la utilidad de línea de comandos. Además, puede usar esta herramienta para comprobar, por ejemplo, compatibilidad y disponibilidad.

> [!TIP]
> ¿No se puede encontrar SqlBindR? Probablemente no ha ejecutado el programa de instalación. SqlBindR está disponible solo después de ejecutar el programa de instalación de Machine Learning Server.

1. Abra un símbolo del sistema como administrador y vaya hasta la carpeta que contiene sqlbindr.exe. La ubicación predeterminada es C:\Program Files\Microsoft\MLServer\Setup

2. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
  
   Anote el nombre completo de la instancia como se muestra. Por ejemplo, el nombre de instancia podría ser MSSQL14. MSSQLSERVER para una instancia predeterminada o algo parecido a SERVERNAME. MYNAMEDINSTANCE.

3. Ejecute el **SqlBindR.exe** comando con el */enlazar* argumento y especifique el nombre de la instancia para actualizar, con el nombre de instancia que se devolvió en el paso anterior.

   Por ejemplo, para actualizar la instancia predeterminada, escriba:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Cuando haya finalizado la actualización, reinicie el servicio Launchpad asociado a cualquier instancia que se ha modificado.

## <a name="bkmk_Unbind"></a>Revertir o desenlazar una instancia

Puede restaurar una instancia enlazada a una instalación inicial de los componentes de R y Python, es necesario establecida el programa de instalación de SQL Server. Hay tres partes para volver a la del servicio de SQL Server.

+ [Paso 1: Desenlazar de Microsoft Machine Learning Server](#step-1-unbind)
+ [Paso 2: Restaurar la instancia al estado original](#step-2-restore)
+ [Paso 3: Volver a instalar los paquetes que agregan a la instalación](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Paso 1: desenlazar

Tiene dos opciones para deshacer el enlace: vuelva a ejecutar el programa de instalación o usar la utilidad de línea de comandos SqlBindR.

#### <a name="bkmk_wizunbind"></a> Desenlazar mediante el programa de instalación

1. Busque al instalador de Machine Learning Server. Si ha quitado al instalador, es posible que deba volver a descargarla o copiarla desde otro equipo.
2. Asegúrese de ejecutar el programa de instalación en el equipo que tiene la instancia que desea separar.
2. El programa de instalación identifica las instancias locales que son candidatos para deshacer el enlace.
3. Desactive la casilla de verificación situada junto a la instancia que desea volver a la configuración original.
4. Acepte el contrato de licencia. Debe indicar su aceptación de términos de licencia incluso cuando se instala.
5. Haga clic en **Finalizar**. El proceso tarda unos minutos.

#### <a name="bkmk_cmdunbind"></a> Desenlazar mediante la línea de comandos

1. Abra un símbolo del sistema y vaya a la carpeta que contiene **sqlbindr.exe**, como se describe en la sección anterior.

2. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia.

   Por ejemplo, el comando siguiente revierte la instancia predeterminada:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Paso 2: Repare la instancia de SQL Server

Ejecute el programa de instalación de SQL Server para reparar la instancia del motor de base de datos tiene las características de R y Python. Las actualizaciones existentes se conservan, pero si se perdió cualquier servicio de actualizaciones de paquetes de R y Python de SQL Server, este paso aplica a las revisiones.

Como alternativa, esto supone más trabajo, pero podría también totalmente desinstalar y reinstalar la instancia del motor de base de datos y, a continuación, aplique todas las actualizaciones de servicio.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Paso 3: Agregue los paquetes de terceros

Podría haber agregado otros paquetes de código abierto o de terceros a la biblioteca del paquete. Puesto que el enlace de reversión cambia la ubicación de la biblioteca de paquetes de forma predeterminada, debe volver a instalar los paquetes a la biblioteca que ahora usan R y Python. Para obtener más información, consulte [predeterminado paquetes](installing-and-managing-r-packages.md), [instalar nuevos paquetes de R](install-additional-r-packages-on-sql-server.md), y [instalar nuevos paquetes de Python](../python/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintaxis de comandos de SqlBindR.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parámetros

|Nombre|Descripción|
|------|------|
|*list*| Muestra una lista de todos los identificadores de instancia de SQL Database en el equipo actual.|
|*bind*| Actualiza la instancia de SQL Database especificada a la versión más reciente de R Server y garantiza que la instancia obtenga automáticamente las actualizaciones futuras de R Server.|
|*unbind*|Desinstala la versión más reciente de R Server de la instancia de SQL Database especificada e impide que las actualizaciones futuras de R Server afecten a la instancia.|

<a name="sqlbinder-error-codes"><a/>

## <a name="binding-errors"></a>Errores de enlace

Instalador de SAM y SqlBindR devuelven los siguientes códigos de error y mensajes.

|Código de error  | de mensaje           | Detalles               |
|------------|-------------------|-----------------------|
|Enlazar el error 0 | OK (correcto) | Enlace que se pasa sin errores. |
|Enlazar error 1 | Argumentos no válidos | Error de sintaxis. |
|Enlazar error 2 | Acción no válida | Error de sintaxis. |
|Enlazar error 3 | Instancia no válida | Una instancia existe, pero no es válida para el enlace. |
|Enlazar error 4 | No se puede enlazar | |
|Enlazar el error 5 | Ya se ha enlazado | Ha ejecutado el comando *bind* , pero la instancia especificada ya está enlazada. |
|Enlazar error 6 | Error de enlace | Se produjo un error al desenlazar la instancia. Este error puede producirse si se ejecuta al instalador MLS sin seleccionar ninguna característica. El enlace requiere que seleccione una instancia MSSQL y R y Python, suponiendo que la instancia es SQL Server 2017. Este error también se produce si SqlBindR no pudo escribir en la carpeta archivos de programa. Las sesiones abiertas o identificadores de SQL Server provocará este error puede producirse. Si recibe este error, reinicie el equipo y los pasos de enlace de puesta al día antes de iniciar cualquier sesión nueva.|
|Enlazar error 7 | No está enlazado | La instancia del motor de base de datos tiene R Services o SQL Server Machine Learning Services. La instancia no está enlazada a Microsoft Machine Learning Server. |
|Enlazar error 8 | Desenlazar error | Se produjo un error al desenlazar la instancia. |
|Enlazar error 9 | No se encontraron instancias | No se encontraron ninguna instancia del motor de base de datos en este equipo. |

## <a name="known-issues"></a>Problemas conocidos

Esta sección enumeran los problemas conocidos específicos para usar de la utilidad SqlBindR.exe o a las actualizaciones de Machine Learning Server que podrían afectar a las instancias de SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restauración de paquetes que estaban previamente instalados

Si ha actualizado a Microsoft R Server 9.0.1, la versión de SqlBindR.exe para esa versión no se pudo restaurar los paquetes originales o los componentes de R por completo, que requieren que el usuario ejecute la reparación de SQL Server en la instancia, aplican a todas las versiones de servicio y, a continuación, reinicie la instancia.

Una versión posterior de SqlBindR automáticamente restaurar las características de R originales, lo que elimina la necesidad de volver a instalar los componentes de R o volver a revisar el servidor. Sin embargo, debe instalar las actualizaciones de paquetes de R que es posible que se han agregado después de la instalación inicial.

Si ha usado las funciones de administración de paquetes para instalar y compartir el paquete, esta tarea es mucho más fácil: puede usar comandos de R para sincronizar los paquetes instalados en el sistema de archivos con registros de la base de datos y viceversa. Para obtener más información, consulte [administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas con varias actualizaciones de SQL Server

Si anteriormente ha actualizado una instancia de SQL Server 2016 R Services a la versión 9.0.1, al ejecutar el nuevo instalador de Microsoft R Server 9.1.0, muestra una lista de todas las instancias válidas y, a continuación, de forma predeterminada, selecciona instancias previamente enlazadas. Si continúa, las instancias previamente enlazadas son independientes. Como resultado, el 9.0.1 anterior se quita la instalación, los incluidos relacionados con los paquetes, pero no se instala la nueva versión de Microsoft R Server (9.1.0).

Como alternativa, puede modificar la instalación existente de R Server como sigue:
1. En el Panel de Control, abra **agregar o quitar programas**.
2. Busque Microsoft R Server y haga clic en **cambiar o modificar**.
3. Cuando se inicia el programa de instalación, seleccione las instancias que desea enlazar a 9.1.0.

Microsoft Machine Learning Server 9.2.1 y 9.3 no tiene este problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Enlazar o desenlazar deja varias carpetas temporales

A veces el enlace y las operaciones de separación no limpiar carpetas temporales.
Si ve carpetas con un nombre de esta manera, puede quitar una vez completada la instalación: R_SERVICES_<guid>

> [!NOTE]
> Asegúrese de esperar hasta que finalice la instalación. Puede tardar mucho tiempo para quitar las bibliotecas de R asociadas con una versión y, a continuación, agregar las nuevas bibliotecas de R. Cuando se complete la operación, se quitan las carpetas temporales.

## <a name="see-also"></a>Vea también

+ [Instale Machine Learning Server para Windows (conectado a Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instale Machine Learning Server para Windows (sin conexión)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas conocidos de Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anuncios de características de la versión anterior de R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Características en desuso, no incluidas o modificadas](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
