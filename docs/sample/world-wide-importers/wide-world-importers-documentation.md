---
title: "Documentación de Wide World Importers | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00c70ac3c82cc5a2e21a687a21c51739b75909ef
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="wide-world-importers-documentation"></a>Documentación de Wide World Importers
Wide World Importers es la nueva base de datos de ejemplo para SQL Server 2016 y base de datos de SQL Azure. Ilustra las capacidades básicas de SQL Server 2016 y base de datos de SQL Azure, para el procesamiento de transacciones (OLTP), almacenamiento de datos y cargas de trabajo de análisis (OLAP), así como híbrido de transacciones y las cargas de trabajo de procesamiento (HTAP) de análisis.

## <a name="about-this-sample"></a>Acerca de este ejemplo

Wide World Importers es un ejemplo completo de la base de datos que muestra el diseño de la base de datos y muestra cómo se pueden aprovechar las características de SQL Server en una aplicación.

Tenga en cuenta que el ejemplo está diseñado para ser representativos de una base de datos típico. No incluye todas las características de SQL Server. El diseño de la base de datos sigue un conjunto común de estándares, pero hay muchas maneras uno podría crearse una base de datos.

**Última versión**: [wide world importers versión](http://go.microsoft.com/fwlink/?LinkID=800630)

**El código para el ejemplo de fuente**: [importadores de todo el mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers).

**Comentarios**: envíe a [ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com).

La documentación para el ejemplo se organiza del siguiente modo:

## <a name="overview"></a>Información general

Información general de la compañía de ejemplo Wide World Importers y los flujos de trabajo mencionados en el ejemplo.

## <a name="main-oltp-database-wideworldimporters"></a>WideWorldImporters de base de datos OLTP principal

Instrucciones para la instalación y configuración del núcleo de la base de datos WideWorldImporters que se usa para el procesamiento de transacciones (OLTP - OnLine Transaction Processing) y los análisis operativos (HTAP - procesamiento transaccional/analítico de híbrida).

Descripción de los esquemas y tablas utilizadas en la base de datos WideWorldImporters.  

Describe cómo WideWorldImporters aprovecha las características de SQL Server core.

Consultas de ejemplo para la base de datos WideWorldImporters.

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>WideWorldImportersDW de la base de datos de análisis y almacenamiento de datos

Instrucciones para la instalación y configuración de OLAP WideWorldImportersDW de la base de datos.

Descripción de los esquemas y tablas utilizadas en la base de datos WideWorldImportersDW, que es la base de datos de ejemplo para almacenamiento de datos y el procesamiento de análisis (OLAP).

Flujo de trabajo para el proceso ETL (extracción, transformación, carga) que migra los datos de la base de datos transaccional WideWorldImporters en el almacén de datos WideWorldImportersDW.

Describe cómo el WideWorldImportersDW aprovecha las características de SQL Server para realizar procesamiento analítico.

Consultas de análisis de ejemplo que aprovecha la base de datos de WideWorldImportersDW.

## <a name="data-generation"></a>Generación de datos

Describe los datos adicionales se pueden generar en la base de datos de ejemplo, por ejemplo Insertar ventas y comprar datos hasta la fecha actual.

