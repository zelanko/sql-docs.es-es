---
title: Opciones (resultados de la consulta-SQL Server-multiservidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.multiserverresultssettings
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLMultiServerResults
ms.assetid: d6768bd8-9cb5-4606-a726-a33a1df9e1bb
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6019a328463d27b4495ae0db70e844eb4e05d747
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089966"
---
# <a name="options-query-results-sql-server-multi-server"></a>Opciones (Resultados de la consulta/SQL Server/Multiservidor)
  Cuando esté consultando varios servidores al mismo tiempo, utilice esta página para especificar las opciones para mostrar los conjuntos de resultados. Mezclar resultados combina los conjuntos de resultados de todos los servidores en un conjunto de resultados único. Cuando se mezclan resultados, el primer servidor en responder establece el esquema para el conjunto de resultados. Para mezclar los conjuntos de resultados, la consulta debe devolver el mismo número de columnas con los mismos nombres de columna de cada servidor. Cuando se mezclan resultados, se muestra un mensaje para cada servidor que no coincide con el esquema (recuento de columna y nombres de columna) que es devuelto por el primer servidor que devuelve resultados.  
  
 Cuando no se mezclan resultados, el conjunto de resultados de cada servidor se mostrará en su propia cuadrícula con su propio esquema.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Mezclar resultados**  
 Active esta casilla para combinar los conjuntos de resultados de varios servidores en la misma cuadrícula.  
  
 **Agregar nombre de servidor a los resultados**  
 Active esta casilla para incluir una columna adicional que proporcione el nombre del servidor que generó cada fila.  
  
 **Agregar nombre de inicio de sesión a los resultados**  
 Active esta casilla para incluir una columna adicional que proporcione el inicio de sesión que se utilizó para conectarse al servidor que proporcionó cada fila.  
  
## <a name="see-also"></a>Consulte también  
 [Cree un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)   
 [Ejecutar instrucciones con varios servidores simultáneamente &#40;SQL Server Management Studio&#41;](../ssms/register-servers/execute-statements-against-multiple-servers-simultaneously.md)  
  
  
