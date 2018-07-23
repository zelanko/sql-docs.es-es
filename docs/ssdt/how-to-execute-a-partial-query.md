---
title: Ejecución de una consulta parcial | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1c6ed1362f7001a55b74538c165b373364b93df3
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087477"
---
# <a name="how-to-execute-a-partial-query"></a>Cómo: Ejecutar una consulta parcial
El Editor de Transact\-SQL le permite resaltar un segmento específico de script y ejecutarlo como una única consulta. Esto simplifica la depuración de secciones de consultas complejas.  
  
> [!WARNING]  
> El procedimiento siguiente usa entidades creadas en procedimientos anteriores de las secciones [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md) y [Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-partially-execute-a-query"></a>Para ejecutar parcialmente una consulta  
  
1.  En el **Explorador de objetos de SQL Server**, haga doble clic en **PerishableFruits** en **Vistas** para abrirlo en el editor de Transact\-SQL.  
  
2.  Resalte el segmento `SELECT p.Id, p.Name FROM dbo.Product p` del código, haga clic con el botón derecho y seleccione **Ejecutar consulta**.  
  
3.  Observe que todas las filas con los campos especificados de la tabla `Products` se devuelven en el panel **Resultados**.  
  
