---
title: Crear un informe de tabla básico (Tutorial de SSRS) | Microsoft Docs
description: Use la herramienta Diseñador de informes de Visual Studio o SQL Server Data Tools (SSDT) y, después, cree un informe paginado de SQL Server Reporting Services (SSRS).
ms.date: 04/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f1549d3ba775d598902fd0fd4b5cc33bab2f54de
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245144"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>Crear un informe de tabla básico (Tutorial de SSRS)

En este tutorial, usará la herramienta *Diseñador de informes* en Visual Studio o SQL Server Data Tools (SSDT). Creará un informe paginado de SQL Server Reporting Services (SSRS). El informe contiene una tabla de consulta, creada a partir de los datos de la base de datos AdventureWorks2016.

A medida que avance en este tutorial, aprenderá cómo:
  
- Crear un proyecto de informe
- Configurar una conexión de datos
- Definir una consulta
- Agregar una región de datos de tabla
- Dar formato al informe
- Agrupar y totalizar los campos
- Obtener una vista previa del informe
- Publicar el informe si lo desea

## <a name="requirements"></a>Requisitos

Para utilizar este tutorial, el sistema debe tener instalados los siguientes componentes:

- Motor de base de datos de [!INCLUDE[msconame-md](../includes/msconame-md.md)] SQL Server.  
- SQL Server 2016 Reporting Services o versiones posteriores (SSRS).
- La base de datos AdventureWorks2016.  Para más información, vea [Adventure Works Sample Databases](https://github.com/Microsoft/sql-server-samples/releases) (Bases de datos de ejemplo de AdventureWorks).
- [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) para Visual Studio junto con la extensión de Reporting Services instalada para permitir el acceso al *Diseñador de informes*.
  
También debe disponer de permisos de solo lectura para recuperar datos de la base de datos AdventureWorks2016.

**Tiempo estimado para completar este tutorial:** 30 minutos.

## <a name="next-steps"></a>Pasos siguientes

[Lección 1: Creación de un proyecto de servidor de informes &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)

[Lección 2: Especificación de información de conexión &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)

[Lección 3: Definición de un conjunto de datos para el informe de tabla &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)

[Lección 4: Adición de una tabla al informe &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)

[Lección 5: Aplicación de formato a un informe &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)

[Lección 6: Adición de grupos y totales &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)

## <a name="see-also"></a>Consulte también

[Tutoriales de Reporting Services](reporting-services-tutorials-ssrs.md) ¿Más preguntas? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
