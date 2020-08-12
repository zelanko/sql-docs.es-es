---
title: Clasificación y detección de datos en SqlClient
description: Describe cómo comprobar si una base de datos de SQL Server admite la clasificación de datos y cómo obtener acceso a la información de clasificación de datos a través de un objeto SqlDataReader.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 27b9c232fe785d3c016848f3bb952236b8e7cd75
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110160"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Clasificación y detección de datos en SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La [clasificación y detección de datos](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017) es un conjunto de servicios avanzados para detectar, clasificar, etiquetar y notificar información confidencial en las bases de datos. SqlClient proporciona una API que expone información de clasificación y detección de datos de solo lectura cuando el origen subyacente es compatible con la característica. Se obtiene acceso a esta información a través de SqlDataReader.

En esta aplicación de ejemplo se muestra cómo acceder a las propiedades de clasificación de datos de SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte también**  

 [Características de SQL Server y ADO.NET](sql-server-features-adonet.md)   
