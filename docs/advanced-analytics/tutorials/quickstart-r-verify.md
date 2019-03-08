---
title: Guía de inicio rápido para comprobar R existe en SQL Server
description: Guía de inicio rápido para comprobar que existen R y Machine Learning Services en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0f461a00c1b9ecca1569b2b4f6257966c075491c
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579695"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Inicio rápido: Comprobación de que R existe en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server incluye compatibilidad con el lenguaje R para el análisis de ciencia de datos de datos residentes de SQL Server. El script de R puede constar de funciones de R de código abierto, bibliotecas de R de terceros o las bibliotecas integradas de Microsoft R como [RevoScaleR](../r/revoscaler-overview.md) para realizar análisis predictivos a escala.

Ejecución del script es a través de procedimientos almacenados, mediante cualquiera de los métodos siguientes:

+ Integrada [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimiento almacenado, pasando el script de R en como un parámetro de entrada.
+ Ajustar el script de R en un [procedimientos almacenados personalizados](sqldev-in-database-r-for-sql-developers.md) que cree.

En este tutorial, comprobará que [Machine Learning Services de SQL Server 2017](../what-is-sql-server-machine-learning.md) o [SQL Server 2016 R Services](../r/sql-server-r-services.md) está instalado y configurado.

## <a name="prerequisites"></a>Requisitos previos

Este ejercicio requiere acceso a una instancia de SQL Server con uno de los siguientes ya instalados:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md), con el lenguaje R instalado
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

Puede ser la instancia de SQL Server en una máquina virtual de Azure o localmente. Tenga presente que la característica de scripting externa está deshabilitada de forma predeterminada, por lo que es posible que deba [habilite los scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y compruebe que **servicio Launchpad de SQL Server** se está ejecutando antes de empezar.

También necesita una herramienta para ejecutar consultas SQL. Puede ejecutar los scripts de R mediante cualquier administración de bases de datos o herramienta de consulta, siempre se puede conectar a una instancia de SQL Server y ejecutar una consulta de Transact-SQL o procedimiento almacenado. Este tutorial rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Compruebe que existe de R

Puede confirmar que los servicios de Machine Learning (con R) está habilitado para la instancia de SQL Server y se instala la versión de R. Siga los pasos siguientes.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server.

2. Ejecute el código siguiente. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print` función devuelve la versión para el **mensajes** ventana. En la salida de ejemplo siguiente, puede ver que SQL Server en este caso tiene R versión 3.3.3 instalado.

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

Si recibe errores de esta consulta, descartar cualquier problema de instalación. Configuración posterior a la instalación es necesario para habilitar el uso de bibliotecas de código externo. Consulte [instalar SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) o [instalar SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Del mismo modo, asegúrese de que se está ejecutando el servicio Launchpad.

En función del entorno, puede que tenga que habilitar las cuentas de trabajo de R para conectarse a SQL Server, instalar bibliotecas de red adicionales, habilitar la ejecución remota de código o reiniciar la instancia una vez configurado todo. Para obtener más información, consulte [R servicios de instalación y actualización de preguntas más frecuentes sobre](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Paquetes de R de lista

Microsoft proporciona una serie de paquetes de R preinstalados con Machine Learning Services en la instancia de SQL Server. Para ver una lista de que R se instalan paquetes, incluidos la versión, dependencias, licencia y obtener información de ruta de acceso de biblioteca, siga estos pasos.

1. Ejecute el siguiente script en la instancia de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. La salida es de `installed.packages()` en R y se devuelve como resultado un conjunto.

    **Resultado**

    ![Los paquetes instalados en R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha confirmado que la instancia está lista para trabajar con R, eche un vistazo más de cerca en una interacción básica de R.

> [!div class="nextstepaction"]
> [Inicio rápido: Script de R "Hello world" en SQL Server](quickstart-r-run-using-tsql.md)
