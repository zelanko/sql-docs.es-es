---
title: Inicio rápido para comprobar que Python existe en SQL Server
description: Guía de inicio rápido para comprobar que Python y Machine Learning Services existen en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98e89cf61e5c53793108a455873382da00a8ea35
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715455"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Inicio rápido: Comprobación de que Python existe en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server incluye compatibilidad con el lenguaje Python para el análisis de ciencia de datos en datos de SQL Server residentes. La ejecución de scripts se realiza a través de procedimientos almacenados, mediante cualquiera de los métodos siguientes:

+ Procedimiento almacenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) integrado, pasando el script de Python en como parámetro de entrada.
+ Ajuste el script de Python en un [procedimiento almacenado personalizado](sqldev-in-database-r-for-sql-developers.md) que cree.

En esta guía de inicio rápido, comprobará que [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) está instalado y configurado.

## <a name="prerequisites"></a>Requisitos previos

Este ejercicio requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) instalado.

La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

También necesita una herramienta para ejecutar consultas SQL. Puede ejecutar los scripts de Python con cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Comprobar que Python existe

Puede confirmar que Machine Learning Services (está habilitado para la instancia de SQL Server y qué versión de Python está instalada. Siga los pasos que se indican a continuación.

1. Abra SQL Server Management Studio y conéctese a su instancia de SQL Server.

2. Ejecute el código siguiente. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. La función `print` de Python devuelve la versión a la ventana **mensajes** . En la salida de ejemplo siguiente, puede ver que SQL Server en este caso tienen instalado Python versión 3.5.2.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Si recibe errores, puede hacer una serie de cosas para asegurarse de que la instancia y Python pueden comunicarse.

En primer lugar, destaque los problemas de instalación. La configuración posterior a la instalación es necesaria para habilitar el uso de bibliotecas de código externo. Vea [instalar Machine Learning Services de SQL Server](../install/sql-machine-learning-services-windows-install.md). Del mismo modo, asegúrese de que el servicio Launchpad se está ejecutando.

También debe agregar el grupo `SQLRUserGroup` de usuarios de Windows como un inicio de sesión en la instancia de, para asegurarse de que Launchpad pueda proporcionar comunicación entre Python y SQL Server. (El mismo grupo se usa para la ejecución de código de R y Python). Para obtener más información, vea [crear un inicio de sesión para SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md).

Además, es posible que tenga que habilitar los protocolos de red que se han deshabilitado, o bien abrir el firewall para que SQL Server pueda comunicarse con los clientes externos. Para obtener más información, consulte [solución de problemas de configuración](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Llamar a funciones revoscalepy

Para comprobar que **revoscalepy** está disponible, ejecute un script de ejemplo que incluya [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) que genere datos de Resumen estadísticos. En el siguiente script se muestra cómo recuperar un archivo de datos. xdf de ejemplo a partir de ejemplos integrados incluidos en revoscalepy. La función RxOptions proporciona el parámetro **sampleDataDir** que devuelve la ubicación de los archivos de ejemplo.

Dado que rx_summary devuelve un objeto de `class revoscalepy.functions.RxSummary.RxSummaryResults`tipo, que contiene varios elementos, puede usar pandas para extraer solo la trama de datos en formato tabular.

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

## <a name="list-python-packages"></a>Enumeración de paquetes de Python

Microsoft proporciona una serie de paquetes de Python preinstalados con Machine Learning Services en la instancia de SQL Server. Para ver una lista de los paquetes de Python instalados, incluida la versión, siga los pasos que se indican a continuación.

1. Ejecute el siguiente script en la instancia de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. El resultado es de `pip.get_installed_distributions()` en Python y se devuelve `STDOUT` como mensajes.

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

Ahora que ha confirmado que la instancia está lista para trabajar con Python, eche un vistazo más de cerca a una interacción básica de Python.

> [!div class="nextstepaction"]
> [Inicio rápido: Script de Python "Hello World" en SQL Server](quickstart-python-run-using-t-sql.md)
