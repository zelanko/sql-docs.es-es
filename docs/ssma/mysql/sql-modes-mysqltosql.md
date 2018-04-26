---
title: Modos SQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12dbdec5d9c56f70e44933a4031c55c5e0b518a1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="sql-modes-mysqltosql"></a>Modos SQL (MySQLToSQL)
SSMA para MySQL puede funcionar en diferentes modos de SQL y puede aplicar estos modos de manera diferente para distintos clientes.  
  
Modos de definen la sintaxis SQL que debe ser compatibles con MySQL y el tipo de validación de datos comprueba que debe realizar. Así resulta más fácil utilizar MySQL en diferentes entornos y utilizar MySQL con SQL Server.  
  
## <a name="sql-modes-grid"></a>Cuadrícula de modos SQL:  
  
-   Cuadrícula de modos de SQL en el nivel de raíz contiene las columnas siguientes: **nombre de modo de SQL**, **cargado modos de SQL**, y **efectivo modos de SQL**.  
  
-   Cuadrícula de modos de SQL en bases de datos categoría, base de datos, tabla categoría, categoría de instrucciones, categoría de vistas, tabla, vista, funciones, procedimientos, UDF y nivel de objeto de evento contiene las columnas siguientes: **nombre de modo de SQL**, **heredarse SQL modos**, y **efectivo modos de SQL**.  
  
-   Cuadrícula de modos de SQL en el nivel de procedimiento almacenado, función almacenado y desencadenador contiene las columnas siguientes: **nombre de modo de SQL**, **Original modos SQL**, y **efectivo modos de SQL**.  
  
> [!NOTE]  
> Modos de grupo se mostrará en negrita, en la columna 'Nombre de modo SQL'.  
  
## <a name="loaded-sql-modes"></a>Modos de SQL cargado  
Se trata de los modos de SQL, que se establecen en el nivel de sesión o raíz. Los modos de SQL una vez cargados en la base de datos de destino no puede editarse o modificarse.  
  
## <a name="inherited-sql-modes"></a>Modos de SQL heredados  
Se trata de los modos de SQL, que se heredan del nodo primario correspondiente.  
  
Excepto para la categoría de funciones, procedimientos, categoría, categoría de eventos y desencadenadores, estos modos de SQL están presentes en todos los niveles (objeto de base de datos, tabla categoría, categoría de instrucciones, vistas categoría, tabla, vista, funciones, procedimientos, UDF y eventos).  
  
> [!NOTE]  
> Si selecciona el **heredar de primario** casilla de verificación, heredarse modos de SQL se puede heredar desde el nodo primario. De forma predeterminada, esta casilla permanece seleccionada.  
  
## <a name="original-sql-modes"></a>Modos SQL originales  
Se trata de los modos de SQL está presente sólo en función, procedimiento y desencadenador niveles.  
  
> [!NOTE]  
> Si selecciona el **original de uso** comprobar cuadro, los modos de SQL que se usaron originalmente en la función correspondiente o se puede utilizar el procedimiento o desencadenador. De forma predeterminada, esta casilla permanece seleccionada.  
  
## <a name="effective-sql-modes"></a>Modos de efectivo SQL  
Modos eficaz de SQL se pueden definir en distintos niveles de la manera siguiente:  
  
-   **En el nivel de sesión:**  
  
    1.  Todos los modos de SQL de carga se puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, los modos SQL efectivo pueden directamente y de forma explícita modificarse.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo de carga de SQL y finalmente se aplica al objeto.  
  
-   **En el nivel de función o procedimiento o desencadenador:**  
  
    1.  Todos los modos de SQL Original se puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, el modo eficaz de SQL puede explícitamente modificarse solo cuando la **original de uso** casilla esté desactivada.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo Original de SQL y finalmente se aplica al objeto.  
  
-   **En los nodos que no son de nivel de función o procedimiento o desencadenador:**  
  
    1.  Todos los modos de SQL de heredada puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, el modo eficaz de SQL puede explícitamente modificarse solo cuando la **heredar de primario** casilla esté desactivada.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo heredado de SQL y por último se aplica al objeto.  
  
