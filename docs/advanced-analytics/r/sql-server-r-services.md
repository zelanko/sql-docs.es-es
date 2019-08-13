---
title: ¿Qué es SQL Server los servicios de R 2016?
titleSuffix: ''
description: R Services es una característica de SQL Server 2016 que ofrece la posibilidad de ejecutar scripts de R con datos relacionales. Puede usar los paquetes y marcos de código abierto y los paquetes de Microsoft R para el análisis predictivo y el aprendizaje automático. Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 973c09be9cff6e66043b056e1a772ab8974cebb4
ms.sourcegitcommit: 12b7e3447ca2154ec2782fddcf207b903f82c2c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957491"
---
# <a name="what-is-sql-server-2016-r-services"></a>¿Qué es SQL Server los servicios de R 2016?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services es una característica de SQL Server 2016 que ofrece la posibilidad de ejecutar scripts de R con datos relacionales. Puede usar los paquetes y marcos de código abierto y los paquetes de [Microsoft R](#packages) para el análisis predictivo y el aprendizaje automático. Los scripts se ejecutan en la base de datos sin mover los datos fuera de SQL Server o a través de la red. En este artículo se explican los conceptos básicos de SQL Server R Services.

> [!Note]
> Se ha cambiado el nombre de R Services a [Machine Learning Services](../what-is-sql-server-machine-learning.md) en SQL Server 2017 y versiones posteriores, y es compatible con Python y R.

## <a name="what-is-r-services"></a>¿Qué es R Services?

SQL Server R Services permite ejecutar scripts de R en la base de datos. Puede utilizarlo para preparar y limpiar los datos, realizar ingeniería de características y entrenar, evaluar e implementar modelos de aprendizaje automático en una base de datos. La característica ejecuta los scripts donde residen los datos y elimina la transferencia de los datos a través de la red a otro servidor.

Las distribuciones base de R se incluyen en R Services. Puede usar paquetes y marcos de código abierto además de los paquetes de Microsoft [RevoScaleR](../r/ref-r-revoscaler.md), [MicrosoftML](../r/ref-r-microsoftml.md), [olapr]. /r/Ref-r-olapr.MD) y [sqlrutils](../r/ref-r-sqlrutils.md) para r.

R Services usa un marco de extensibilidad para ejecutar scripts de R en SQL Server. Más información sobre cómo funciona:

+ [Marco de extensibilidad](../concepts/extensibility-framework.md)
+ [Extensión de R](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>¿Qué puedo hacer con R Services?

Puede usar R Services para crear y entrenar modelos de aprendizaje automático y aprendizaje profundo en SQL Server. También puede implementar modelos existentes en R Services y usar datos relacionales para las predicciones.

Entre los ejemplos del tipo de predicciones que puede usar SQL Server R Services para, se incluyen:

|||
|-|-|
|Clasificación/categorización|Dividir automáticamente los comentarios de los clientes en categorías positivas y negativas|
|Valores continuos de regresión y predicción|Predecir el precio de las casas en función del tamaño y la ubicación|
|Detección de anomalías|Detectar transacciones bancarias fraudulentas |
|Recomendaciones|Sugiera productos que los compradores en línea pueden querer comprar, en función de las compras anteriores|

### <a name="how-to-execute-r-scripts"></a>Cómo ejecutar scripts de R

Hay dos maneras de ejecutar scripts de R en R Services:

+ La manera más común es usar el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)de T-SQL.

+ También puede usar el cliente de R preferido y escribir scripts que inserten la ejecución (denominada *contexto de cálculo remoto*) en un SQL Server remoto. Vea cómo [configurar un desarrollo de R de cliente de ciencia de datos](../r/set-up-a-data-science-client.md) para obtener más información.

<a name="packages"></a>

## <a name="r-packages"></a>Paquetes de R

Puede usar los paquetes y marcos de código abierto, además de los paquetes de empresa de Microsoft. Los paquetes de R de código abierto más comunes están preinstalados en R Services. También se incluyen los siguientes paquetes de R de Microsoft:

| Paquete | Descripción |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | Paquete principal para transformaciones y manipulaciones de datos de R escalables, resumen estadístico, visualización y muchas formas de modelado. Además, las funciones de este paquete distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para el procesamiento en paralelo. |
| [MicrosoftML (R)](../r/ref-r-microsoftml.md) | Agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. |
| [olapR](../r/ref-r-olapr.md) | Funciones de R utilizadas para las consultas MDX en un cubo OLAP de SQL Server Analysis Services. |
| [sqlrutils](../r/ref-r-sqlrutils.md) | Un mecanismo para usar scripts de R en un procedimiento almacenado de T-SQL, registrar ese procedimiento almacenado en una base de datos y ejecutar el procedimiento almacenado desde un [entorno de desarrollo de R](../r/set-up-a-data-science-client.md). |
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) es la distribución mejorada de R de Microsoft. Es una plataforma de código abierto completa para el análisis estadístico y la ciencia de datos. Se basa en y 100% compatible con R e incluye capacidades adicionales para mejorar el rendimiento y la reproducibilidad. |

## <a name="how-do-i-get-started-with-rservices"></a>Cómo Introducción a RServices?

1. [Instalación de SQL Server R Services de 2016](../install/sql-r-services-windows-install.md)

1. Configure las herramientas de desarrollo. Puede usar:

    + [Azure Data Studio](../../azure-data-studio/what-is.md) o [SQL Server Management Studio (SSMS)](../../ssms/sql-server-management-studio-ssms.md) para usar T-SQL y el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para ejecutar el script de R.
    + R en su propio equipo portátil o estación de trabajo de desarrollo para ejecutar scripts. Puede extraer datos de forma local o insertar la ejecución de forma remota en SQL Server con [RevoScaleR](../r/ref-r-revoscaler.md). Vea cómo [configurar un desarrollo de R de cliente de ciencia de datos](../r/set-up-a-data-science-client.md) para obtener más información.

1. Escritura del primer script de R

    + Inicio rápido: [Ejecutar un script "Hello World" en R](../tutorials/quickstart-r-run-using-tsql.md)
    + Inicio rápido: [Crear un modelo predictivo en R](../tutorials/quickstart-r-create-predictive-model.md)
    + Tutorial: [Uso de R en T-SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md): Explorar datos, realizar ingeniería de características, entrenar e implementar modelos y realizar predicciones (serie de cinco partes)
    + Tutorial: [Usar r Services en herramientas de r](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): Explorar datos, crear gráficos y trazados, realizar ingeniería de características, entrenar e implementar modelos y realizar predicciones (serie de seis partes)

## <a name="next-steps"></a>Pasos siguientes

+ [Instalación de SQL Server R Services de 2016](../install/sql-r-services-windows-install.md)
+ [Configuración de un cliente de ciencia de datos para el desarrollo de R](../r/set-up-a-data-science-client.md)