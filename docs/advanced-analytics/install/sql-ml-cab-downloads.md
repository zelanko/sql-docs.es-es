---
title: Descarga de actualizaciones para la instalación sin conexión
description: Descargue los archivos de paquete y CAB de R y Python para SQL Server Machine Learning Services y SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e7266d90e04071c242145fc0df2e59ce86d86a16
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727627"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Descargas de CAB para actualizaciones acumulativas de instancias de análisis en base de datos de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Las instancias de SQL Server que están configuradas para análisis en base de datos incluyen características de R y Python. Estas características se incluyen en archivos CAB, se instalan y prestan servicio a través de la configuración de SQL Server. En los dispositivos conectados a Internet, las actualizaciones de CAB se aplican normalmente a través de Windows Update. En los servidores desconectados, los archivos CAB deben descargarse y aplicarse manualmente. 

En este artículo se proporcionan vínculos de descarga a archivos CAB para cada actualización acumulativa. Para obtener más información sobres las instalaciones sin conexión, vea [Instalación de componentes de aprendizaje automático de SQL Server sin acceso a Internet](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Prerequisites

Comience con una instalación de línea base.

+ En SQL Server Machine Learning Services, la versión inicial es la instalación de línea base. 
+ En SQL Server 2016 R Services, puede comenzar con la versión inicial, SP1 o SP2. 

También puede aplicar las actualizaciones acumulativas a un servidor independiente.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>CAB de SQL Server 2017

Los archivos CAB se enumeran en orden cronológico inverso. Cuando descargue los archivos CAB y los transfiera al equipo de destino, colóquelos en una carpeta adecuada, como **Descargas** o la carpeta %temp% del usuario de instalación.

|Versión  |Componente | Vínculo de descarga  | Problemas tratados | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| Los binarios del paquete están ahora firmados. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| Los binarios del paquete están ahora firmados. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| Los binarios del paquete están ahora firmados. |
| | Servidor de Python    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| Los binarios del paquete están ahora firmados.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contiene una corrección para actualizar un [R Server con operaciones independientes](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), como se instala a través de la configuración del SQL Server. Use la CAB CU13 y siga [estas instrucciones](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar la actualización. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contiene una corrección para actualizar un [Python Server con operaciones independientes](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), como se instala a través de la configuración del SQL Server. Use la CAB CU13 y siga [estas instrucciones](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar la actualización. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correcciones menores.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step pierde el orden de las filas cuando se eliminan los duplicados. <br/>SPEE produce un error en la detección del tipo de datos en el índice de almacén de columnas agrupado. <br/>Devuelve una tabla vacía cuando las columnas contienen todos los valores NULL. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de datos de fecha y hora en la consulta SPEES.<br/>se han mejorado los mensajes de error de microsoftml cuando faltan modelos entrenados previamente.<br/> Correcciones de funciones y variables de transformación de revoscalepy.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Errores relacionados con la ruta de acceso en rxInstallPackages.<br/>Conexiones en un bucle invertido para RxExec.
| | Microsoft Python Open    | No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexiones en un bucle invertido para rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| |  Servidor de Python    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. |
| | Servidor de Python    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Serialización del modelo de Python en revoscalepy con la función [rx_serialize_model function](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>Compatibilidad de la [puntuación nativa](../sql-native-scoring.md), además de mejoras en la [ puntuación en tiempo real](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| No existe ningún cambio con respecto a las versiones anteriores. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| No existe ningún cambio con respecto a las versiones anteriores. | 
| | Servidor de Python    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Agrega rx_create_col_info para devolver información del esquema. <br/>Mejoras en [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para admitir escenarios paralelos mediante el contexto de cálculo de `RxLocalParallel`.|
|**Versión inicial** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Servidor de Python    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>CAB de SQL Server 2016

Para SQL Server 2016 R Services, las versiones de línea base son la versión RTM o una versión del Service Pack.

|Versión  |Vínculo de descarga  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> Al instalar SQL Server 2016 SP1 CU4 o SP1 CU5 sin conexión, descargue SRO_3.2.2.16000_1033.cab. Si descargó SRO_3.2.2.13000_1033.cab de FWLINK 831785 como se indica en el cuadro de diálogo de instalación, cambie el nombre del archivo a SRO_3.2.2.16000_1033.cab antes de instalar la actualización acumulativa.

Si quiere ver el código fuente de Microsoft R, puede descargarlo como archivo en formato .tar: [Descargar los instaladores de R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

[Aplicación de actualizaciones acumulativas en equipos sin acceso a Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicación de actualizaciones acumulativas en equipos que tengan conectividad a Internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicación de actualizaciones acumulativas a un servidor independiente](sql-machine-learning-standalone-windows-install.md#apply-cu)
