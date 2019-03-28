---
title: 'Descargas de CAB para las actualizaciones acumulativas de SQL Server: SQL Server Machine Learning'
description: R y Python CAB y paquete de descarga de SQL Server 2017 Machine Learning Services y SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/19/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 22304bb9ec142e8f0c61797ed6907c0aa78c34f8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511382"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>Descargas de CAB para las actualizaciones acumulativas de análisis en bases de datos de SQL Server de instancias

Las instancias de SQL Server que están configuradas para el análisis en bases de datos incluyen características de R y Python. Estas características se incluyen en los archivos CAB, instalado y atender a través del programa de instalación de SQL Server. En los dispositivos conectados a internet, CAB actualizaciones normalmente se aplican a través de Windows Update. En los servidores sin conexión, deben descargarse archivos CAB y aplica manualmente. 

Este artículo proporcionan vínculos de descarga de archivos .cab para cada actualización acumulativa. Se proporcionan vínculos para SQL Server 2017 Machine Learning Services (R y Python), así como SQL Server 2016 R Services. Para obtener más información sobre las instalaciones sin conexión, consulte [componentes sin acceso a internet de aprendizaje de máquina de instalar SQL Server](sql-ml-component-install-without-internet-access.md#apply-cu).

## <a name="prerequisites"></a>Requisitos previos

Empiece con una instalación de línea de base.

+ En Machine Learning Services de SQL Server 2017, la versión inicial es la instalación de línea de base. 
+ En SQL Server 2016 R Services, puede iniciar con la versión inicial, SP1 o SP2. 

También puede aplicar las actualizaciones acumulativas a un servidor independiente.

## <a name="sql-server-2017-cabs"></a>Archivos CAB SQL Server 2017

Archivos CAB se enumeran en orden cronológico inverso. Al descargar los archivos CAB y transferirlos al equipo de destino, colocarlos en una carpeta adecuada como **descargas** o la carpeta del usuario del programa de instalación % temp %.

|Versión  |Componente | Vínculo de descarga  | Problemas solucionados | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| Contiene una corrección para actualizar una [operacionalizados R Server independiente](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), tal y como se instala a través del programa de instalación de SQL Server. Use los archivos CAB CU13 y siga [estas instrucciones](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar la actualización. |
| | Apertura de Python de Microsoft     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| Contiene una corrección para actualizar una [operacionalizados Server Python independiente](https://docs.microsoft.com/machine-learning-server/what-is-operationalization), tal y como se instala a través del programa de instalación de SQL Server. Use los archivos CAB CU13 y siga [estas instrucciones](sql-machine-learning-standalone-windows-install.md#apply-cu) para aplicar la actualización. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| Correcciones menores.|
| | Apertura de Python de Microsoft     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| Python rx_data_step pierde el orden de fila cuando se quitan los duplicados. <br/>SPEE se produce un error de detección del tipo de datos del índice agrupado. <br/>Devuelve una tabla vacía cuando las columnas contienen todos los valores null. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Apertura de Python de Microsoft     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Apertura de Python de Microsoft     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| Tipos de datos de fecha y hora en la consulta SPEES.<br/>mensajes de error en microsoftml mejorados cuando faltan modelos previamente entrenados.<br/> Correcciones de revoscalepy transforman las funciones y variables.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| Errores de tiempo relacionados con la ruta de acceso en rxInstallPackages.<br/>Conexiones en un bucle invertido para RxExec.
| | Apertura de Python de Microsoft    | Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Conexiones en un bucle invertido para rx_exec.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Apertura de Python de Microsoft     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| |  Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Apertura de Python de Microsoft     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. |
| | Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Serialización en revoscalepy, del modelo de Python mediante el [rx_serialize_model función](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model).<br/>[Puntuación nativa](../sql-native-scoring.md) , además de mejoras en [de puntuación en tiempo real](../real-time-scoring.md). 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| Ningún cambio respecto a versiones anteriores. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Apertura de Python de Microsoft     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| Ningún cambio respecto a versiones anteriores. | 
| | Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | Agrega rx_create_col_info para devolver información de esquema. <br/>Mejoras de [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para admitir escenarios paralelos mediante el `RxLocalParallel` contexto de proceso.|
|**Versión inicial** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Apertura de Python de Microsoft     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>Archivos CAB SQL Server 2016

Para SQL Server 2016 R Services, las versiones de línea de base son la versión RTM o una versión del service pack.

|Versión  |Vínculo de descarga  |
|---------|---------------|
|**SQL Server 2016 SP2 CU1-CU4**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP1 CU4-CU10**     |
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU1-CU3**     |
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
> Al instalar SQL Server 2016 SP1 CU4 o CU5 SP1 sin conexión, descargue SRO_3.2.2.16000_1033.cab. Si descargó SRO_3.2.2.13000_1033.cab desde FWLINK 831785 como se indica en el cuadro de diálogo, cambie el nombre del archivo SRO_3.2.2.16000_1033.cab antes de instalar la actualización acumulativa.

Si desea ver el código fuente de Microsoft R, está disponible para su descarga como un archivo .tar formátu: [Descargue a los instaladores de R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

## <a name="see-also"></a>Vea también

[Aplicar actualizaciones acumulativas en equipos sin acceso a internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar actualizaciones acumulativas en equipos que tienen conectividad a internet](sql-ml-component-install-without-internet-access.md#apply-cu)

[Aplicar actualizaciones acumulativas a un servidor independiente](sql-machine-learning-standalone-windows-install.md#apply-cu)
