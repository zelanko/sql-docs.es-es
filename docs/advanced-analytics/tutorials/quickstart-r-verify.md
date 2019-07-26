---
title: Inicio rápido para comprobar que R existe en SQL Server
description: Inicio rápido para comprobar que R y Machine Learning Services existen en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 951ffc07a32434b2f8d333140445f12c2971b811
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470616"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Inicio rápido: Comprobación de que R existe en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server incluye compatibilidad con el lenguaje R para el análisis de ciencia de datos en datos de SQL Server residentes. El script de R puede constar de funciones de R de código abierto, bibliotecas de R de terceros o bibliotecas de Microsoft R integradas como [RevoScaleR](../r/revoscaler-overview.md) para el análisis predictivo a escala.

La ejecución de scripts se realiza a través de procedimientos almacenados, mediante cualquiera de los métodos siguientes:

+ Procedimiento almacenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) integrado, pasando el script de R en como parámetro de entrada.
+ Ajuste el script de R en un [procedimiento almacenado personalizado](sqldev-in-database-r-for-sql-developers.md) que cree.

En esta guía de inicio rápido, comprobará que [SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md) o [SQL Server 2016 R Services](../r/sql-server-r-services.md) está instalado y configurado.

## <a name="prerequisites"></a>Requisitos previos

Este ejercicio requiere acceso a una instancia de SQL Server con uno de los siguientes elementos ya instalados:

+ [SQL Server Machine Learning Services 2017](../install/sql-machine-learning-services-windows-install.md), con el lenguaje R instalado
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

También necesita una herramienta para ejecutar consultas SQL. Puede ejecutar los scripts de R mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Comprobar que existe R

Puede confirmar que Machine Learning Services (con R) está habilitado para la instancia de SQL Server y qué versión de R está instalada. Siga los pasos que se indican a continuación.

1. Abra SQL Server Management Studio y conéctese a su instancia de SQL Server.

2. Ejecute el código siguiente. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. La función `print` R devuelve la versión a la ventana **mensajes** . En la salida de ejemplo siguiente, puede ver que SQL Server en este caso tienen instalada la versión 3.3.3 de R.

    **Resultado**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

Si obtiene algún error de esta consulta, destaque cualquier problema de instalación. La configuración posterior a la instalación es necesaria para habilitar el uso de bibliotecas de código externo. Consulte [install SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) o [install SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Del mismo modo, asegúrese de que el servicio Launchpad se está ejecutando.

En función del entorno, puede que tenga que habilitar las cuentas de trabajo de R para conectarse a SQL Server, instalar bibliotecas de red adicionales, habilitar la ejecución remota de código o reiniciar la instancia una vez configurado todo. Para obtener más información, consulte [preguntas más frecuentes sobre la instalación y actualización de R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Enumerar paquetes de R

Microsoft ofrece una serie de paquetes de R preinstalados con Machine Learning Services en la instancia de SQL Server. Para ver una lista de los paquetes de R instalados, incluidas la versión, las dependencias, la licencia y la información de la ruta de acceso de la biblioteca, siga estos pasos.

1. Ejecute el siguiente script en la instancia de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. La salida es de `installed.packages()` R y se devuelve como un conjunto de resultados.

    **Resultado**

    ![Paquetes instalados en R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha confirmado que la instancia está lista para trabajar con R, eche un vistazo más de cerca a una interacción básica de R.

> [!div class="nextstepaction"]
> [Inicio rápido: Script R "Hello World" en SQL Server](quickstart-r-run-using-tsql.md)
