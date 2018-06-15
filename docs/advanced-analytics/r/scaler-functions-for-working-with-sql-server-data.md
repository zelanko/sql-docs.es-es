---
title: Funciones de RevoScaleR para trabajar con datos de SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d97a75cdc7da6a05847373b259ef562353d578ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203497"
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>Funciones de RevoScaleR para trabajar con datos de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tema proporciona información general de las principales funciones que se proporcionan en RevoScaleR para trabajar con datos de SQL Server.

Para obtener una lista completa de las funciones ScaleR y cómo usarlas, vea el [Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) referencia.

## <a name="create-sql-server-data-sources"></a>Crear orígenes de datos de SQL Server

Las siguientes funciones permiten definir un origen de datos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Un objeto de origen de datos es un contenedor que especifica una cadena de conexión, junto con el conjunto de datos que quiera, definido como una tabla, una vista o una consulta. No se admiten llamadas a procedimientos almacenados.

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -definir una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] objeto de origen de datos.

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -crear objetos de datos de otras bases de datos ODBC. 

## <a name="perform-ddl-statements"></a>Ejecutar instrucciones de DDL

Puede ejecutar instrucciones de DDL de R, si tiene los permisos necesarios en la instancia y la base de datos. Las siguientes funciones utilizan llamadas ODBC para ejecutar instrucciones de DDL o recuperar el esquema de base de datos.

+ `rxSqlServerTableExists` y [rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -quitar una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de tabla, o bien compruebe la existencia de una tabla de base de datos u objeto

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -ejecutar un comando de lenguaje de definición de datos (DDL) que define o manipula objetos de base de datos. Esta función no puede devolver los datos y sólo se utiliza para recuperar o modificar el esquema de objetos o metadatos.

## <a name="define-or-manage-compute-contexts"></a>Definir o administrar contextos de proceso

Las funciones siguientes permiten definir un nuevo contexto de cálculo, cambiar los contextos de cálculo o identificar el contexto de cálculo actual.

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext): crear un contexto de cálculo.

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver): generar un contexto de cálculo de SQL Server que permite que las funciones de **ScaleR** se ejecuten en SQL Server R Services. Este contexto de cálculo actualmente solo se admite para instancias de SQL Server en Windows.

+ `rxGetComputeContext` y [rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) : obtener o establecer el contexto de computación activa.

## <a name="move-data-and-transform-data"></a>Mover los datos y transformar datos

Una vez haya creado un objeto de origen de datos, puede utilizar el objeto para cargar datos en él, transformar datos o escribir nuevos datos en el destino especificado. En función del tamaño de los datos en el origen, también puede definir el tamaño del lote como parte del origen de datos y mover los datos en fragmentos.

+ [métodos de rxOpen](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods) : Compruebe si hay un origen de datos, abrir o cerrar un origen de datos, leer datos desde un origen, escribir datos en el destino y cerrar un origen de datos

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -mover datos desde un origen de datos en el almacenamiento de archivos o en una trama de datos.

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -transformar datos al mover entre orígenes de datos.

Las siguientes funciones se pueden usar para crear un almacén de datos local en el formato xdf. Este archivo puede ser útil al trabajar con más datos de los que se pueden transferir desde la base de datos en un lote o con más datos de los que caben en la memoria.

Por ejemplo, si suele mover grandes cantidades de datos desde una base de datos a una estación de trabajo local, en lugar de la consulta la base de datos varias veces para cada operación de R, se puede utilizar el archivo xdf. como un tipo de caché para guardar los datos localmente y, a continuación, trabajar con ellos en el área de trabajo de R.

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -crear un objeto de datos xdf.

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -lee los datos en una trama de datos desde un archivo xdf.

Para obtener más información sobre cómo trabajar con estas funciones, incluido el uso de datos de orígenes distintos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [cómo le guía para el análisis de datos en Microsoft R](https://docs.microsoft.com/r-server/r/how-to-introduction).
