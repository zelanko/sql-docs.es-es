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
ms.openlocfilehash: 6d82bfd3c49576a35b24f5a04cdc2c03dceeb766
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081504"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Clasificación y detección de datos en SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La [clasificación y detección de datos](../../../relational-databases/security/sql-data-discovery-and-classification.md) es un conjunto de servicios avanzados para detectar, clasificar, etiquetar y notificar información confidencial en las bases de datos. SqlClient proporciona una API que expone información de clasificación y detección de datos de solo lectura cuando el origen subyacente es compatible con la característica. Se obtiene acceso a esta información a través de SqlDataReader.

En esta aplicación de ejemplo se muestra cómo acceder a las propiedades de clasificación de datos de SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte también**  

 [Características de SQL Server y ADO.NET](sql-server-features-adonet.md)