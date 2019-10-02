---
title: Supervisión de la ejecución de scripts de Python y R mediante informes personalizados en SSMS
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714399"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>Supervisión de la ejecución de scripts de Python y R mediante informes personalizados en SQL Server Management Studio
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use informes personalizados en SQL Server Management Studio (SSMS) para supervisar la ejecución de scripts externos (Python y R), los recursos usados, diagnosticar problemas y ajustar el rendimiento en SQL Server Machine Learning Services.

En estos informes, puede ver detalles como:

- Sesiones activas de Python o R
- Opciones de configuración de la instancia
- Estadísticas de ejecución para trabajos de machine learning
- Eventos extendidos para R Services
- Paquetes de Python o R instalados en la instancia actual

En este artículo se explica cómo instalar y usar los informes personalizados proporcionados para SQL Server Machine Learning Services.

Para obtener más información sobre los informes de SQL Server Management Studio, vea [informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>Cómo instalar los informes

Los informes se diseñan mediante SQL Server Reporting Services, pero se pueden usar directamente desde SQL Server Management Studio. Reporting Services no tiene que estar instalado en la instancia de SQL Server.

Para usar estos informes, siga estos pasos:

1. Descargue los [informes personalizados de SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) para SQL Server Machine Learning Services de github.

2. Copiar los informes en Management Studio

    1. Ubique la carpeta de informes personalizados utilizada por SQL Server Management Studio. De forma predeterminada, los informes personalizados se almacenan en esta carpeta (donde **user_name** es el nombre de usuario de Windows):

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       También puede especificar una carpeta diferente o crear subcarpetas.

    2. Copie el *. Archivos RDL que descargó en la carpeta de informes personalizados.

3. Ejecutar los informes en Management Studio

    1. En Management Studio, haga clic en el nodo **Bases de datos** de la instancia donde quiere ejecutar los informes.

    2. Haga clic en **Informes**y, después, en **Informes personalizados**.

    3. En el cuadro de diálogo **Abrir archivo** , ubique la carpeta de informes personalizados.

    4. Seleccione uno de los archivos RDL que descargó y, luego, haga clic en **Abrir**.

## <a name="reports"></a>Informes

El [repositorio de informes personalizados de SSMS en github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) incluye los siguientes informes:

| Informe | Descripción |
|-|-|
| Sesiones activas | Usuarios que están conectados actualmente a la instancia de SQL Server y que ejecutan un script de Python o R. |
| Configuración | Configuración de la instalación de Machine Learning Services y las propiedades del Runtime de Python o R. |
| Configurar instancia | Configure Machine Learning Services. |
| Estadísticas de ejecución | Estadísticas de ejecución de servicios de Machine Learning. Por ejemplo, puede obtener el número total de ejecuciones de scripts externos y el número de ejecuciones paralelas. |
| Eventos extendidos | Eventos extendidos que están disponibles para obtener más información sobre la ejecución de scripts externos. |
| . | Enumere los paquetes de R o Python instalados en la instancia de SQL Server y sus propiedades, como versión y nombre. |
| Resource Usage | Ver la CPU, la memoria, el consumo de e/s de SQL Server y la ejecución de scripts externos. También puede ver la configuración de memoria para los grupos de recursos externos. |

## <a name="next-steps"></a>Pasos siguientes

- [Supervisar SQL Server Machine Learning Services mediante vistas de administración dinámica (DMV)](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [Eventos extendidos para R Services](../r/extended-events-for-sql-server-r-services.md)
