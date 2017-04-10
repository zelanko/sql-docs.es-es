---
title: "Funciones de utilizar otros equipos para trabajar con datos de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# Funciones de utilizar otros equipos para trabajar con datos de SQL Server
Este tema proporciona una visión general de las funciones principales de utilizar otros equipos para su uso con SQL Server, junto con comentarios en su sintaxis.

Para obtener una lista completa de las funciones de utilizar otros equipos y cómo usarlas, consulte el [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) referencia en la biblioteca MSDN. 

## Funciones para trabajar con orígenes de datos de SQL Server
Las siguientes funciones le permiten definir una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] origen de datos. Un objeto de origen de datos es un contenedor que especifica una cadena de conexión, junto con el conjunto de datos que desee, definido como una tabla, vista o consulta. No se admiten llamadas a procedimientos almacenados.  

Además de definir un origen de datos, puede ejecutar instrucciones de DDL de R, si tiene los permisos necesarios en la instancia y la base de datos. 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -definir una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] objeto de origen de datos
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -quitar una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabla
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -comprobar la existencia de un objeto o una tabla de base de datos
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) : ejecutar un comando para definir, manipular o controlar datos SQL, pero no devuelven datos  

## Funciones para definir o administrar un contexto de cálculo
Las funciones siguientes permiten definir un nuevo contexto de cálculo, cambie los contextos de proceso o identificar el contexto del proceso actual.
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -crear un contexto de cálculo. 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) -generar un contexto de proceso de SQL Server que permite **utilizar otros equipos** ejecutan funciones de R servicios de SQL Server.
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -obtener el contexto del proceso actual. 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -especificar que calcular el contexto que se utiliza. 

## Funciones para usar un origen de datos
Una vez haya creado un objeto de origen de datos, puede abrirlo para obtener datos o escribir nuevos datos en él. Dependiendo del tamaño de los datos en el origen, también puede definir el tamaño del lote como parte del origen de datos y mover los datos en fragmentos. 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -comprobar si un origen de datos está disponible
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -Abrir un origen de datos para la lectura
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -leer datos desde un origen
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -escribir datos en el destino
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -Cerrar un origen de datos

Para obtener más información sobre cómo trabajar con estas funciones de utilizar otros equipos, que puede trabajar con orígenes de datos distintos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], consulte [ R Microsoft Server - Introducción](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Funciones que funcionan con archivos XDF
Las siguientes funciones se pueden usar para crear una caché de datos local en el formato XDF. Este archivo puede ser útil al trabajar con más datos que se puede transferir desde la base de datos en un lote o más datos que caben en la memoria.

Si suele mover grandes cantidades de datos de una base de datos a una estación de trabajo local, en lugar de la consulta la base de datos varias veces para cada operación de R, se puede utilizar el archivo XDF para guardar los datos localmente y, a continuación, trabajar con ellos en el área de trabajo de R, utilizando el archivo XDF como la memoria caché.

+ `rxImport` -Mover datos desde un origen de ODBC en el archivo XDF
+ `RxXdfData` -Crear un objeto de datos XDF
+ `RxDataStep` -Leer datos de int XDF una trama de datos
+ `rxXdfToDataFrame` -Leer datos de XDF en una trama de datos
+ `rxReadXdf` -Lee datos de XDF en una trama de datos

Para obtener un ejemplo de cómo se utilizan los archivos XDF, consulte este tutorial:  [datos ciencia profundización - mediante las funciones de utilizar otros equipos](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

Para obtener más información acerca de estas funciones utilizar otros equipos, que se puede utilizar para transferir datos de muchos orígenes diferentes, consulte[ R Microsoft Server - Introducción](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started).

## Vea también
[Comparación de funciones de utilizar otros equipos y Base R](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
