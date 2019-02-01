---
title: Guía de inicio rápido para comprobar Python existe en SQL Server
description: Guía de inicio rápido para comprobar que existen Python y Machine Learning Services en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b0ef5d33757d9f8c4e3aed53d3867bfd5b1297b2
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513765"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Inicio rápido: Comprobación de que Python existe en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server incluye compatibilidad de lenguaje de Python para análisis de ciencia de datos en los datos de SQL Server residentes. Ejecución del script es a través de procedimientos almacenados, mediante cualquiera de los métodos siguientes:

+ Integrada [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado, pasando el script de Python en como un parámetro de entrada.
+ Ajustar el script de Python en un [procedimientos almacenados personalizados](sqldev-in-database-r-for-sql-developers.md) que cree.

En este tutorial, comprobará que [Machine Learning Services de SQL Server 2017](../what-is-sql-server-machine-learning.md) está instalado y configurado.

## <a name="prerequisites"></a>Requisitos previos

Este ejercicio requiere acceso a una instancia de SQL Server con [Machine Learning Services de SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) instalado.

Puede ser la instancia de SQL Server en una máquina virtual de Azure o localmente. Tenga presente que la característica de scripting externa está deshabilitada de forma predeterminada, por lo que es posible que deba [habilite los scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y compruebe que **servicio Launchpad de SQL Server** se está ejecutando antes de empezar.

También necesita una herramienta para ejecutar consultas SQL. Puede ejecutar los scripts de Python mediante cualquier administración de bases de datos o herramienta de consulta, siempre se puede conectar a una instancia de SQL Server y ejecutar una consulta de Transact-SQL o procedimiento almacenado. Este tutorial rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Compruebe que existe de Python

Puede confirmar que Machine Learning Services (está habilitado para la instancia de SQL Server y se instala la versión de Python. Siga los pasos siguientes.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server.

2. Ejecute el código siguiente. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. La versión de Python `print` función devuelve la versión para el **mensajes** ventana. En la salida de ejemplo siguiente, puede ver que SQL Server en este caso tiene la versión de Python 3.5.2 instalado.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Si se producen errores, hay una variedad de cosas que puede hacer para asegurarse de que la instancia y Python puede comunicarse.

En primer lugar, descartar cualquier problema de instalación. Configuración posterior a la instalación es necesario para habilitar el uso de bibliotecas de código externo. Consulte [instalar SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md). Del mismo modo, asegúrese de que se está ejecutando el servicio Launchpad.

También debe agregar el grupo de usuarios de Windows `SQLRUserGroup` como inicio de sesión en la instancia, para asegurarse de que Launchpad puede proporcionar comunicación entre Python y SQL Server. (El mismo grupo se usa para ambos R y ejecución de código de Python). Para obtener más información, consulte [autenticación implícita habilitada](../security/add-sqlrusergroup-to-database.md).

Además, deberá habilitar los protocolos de red que se han deshabilitado o abrir el firewall para que SQL Server puedan comunicarse con los clientes externos. Para obtener más información, consulte [solucionar problemas de instalación](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Llamar a funciones de revoscalepy

Para comprobar que **revoscalepy** está disponible, ejecute un script de ejemplo que incluye [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) que genera un resumen datos estadísticos. El script siguiente muestra cómo recuperar un archivo de datos de ejemplo xdf de ejemplos integrados incluidos en revoscalepy. La función RxOptions ofrece el **sampleDataDir** parámetro que devuelve la ubicación de los archivos de ejemplo.

Dado que rx_summary devuelve un objeto de tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contiene varios elementos, puede usar pandas para extraer la trama de datos en formato tabular.

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>Enumerar los paquetes de Python

Microsoft proporciona una serie de paquetes de Python preinstalados con Machine Learning Services en la instancia de SQL Server. Para ver una lista de qué Python se instalan paquetes, incluida la versión, siga estos pasos.

1. Ejecute el siguiente script en la instancia de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. La salida es de `pip.get_installed_distributions()` en Python y se devuelven `STDOUT` mensajes.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha confirmado que la instancia está lista para trabajar con Python, eche un vistazo más de cerca en una interacción básica de Python.

> [!div class="nextstepaction"]
> [Inicio rápido: Script de Python "Hello world" en SQL Server ](quickstart-python-run-using-t-sql.md)
